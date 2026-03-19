### Installation
```
pnpm install zod
npm install zod
```

Usage:
### Strings Most Common

``` java
z.string()
z.string().min(3)
z.string().max(100)
z.string().email()
z.string().url()
z.string().uuid()
z.string().regex(/^[A-Z]+$/)
z.string().trim()
```
### Numbers Most Common

``` java
z.number()
z.number().min(0)
z.number().max(100)
z.number().int()
z.number().positive()
z.number().negative()
```
### Booleans | Enum | Dates | Optional Most Common

``` java
z.boolean()

z.enum(["ADMIN", "USER"]),

z.date()
z.string().datetime() // ISO string

z.string().optional()   // undefined allowed
z.string().nullable()   // null allowed
z.string().nullish()    // null + undefined
z.string().default("N/A")
```

## Usage

```java
// common.schema.ts
import { z } from "zod";  
  
export const Email = z.string().email("Invalid email");  
  
export const Password = z  
.string()  
.min(8, "Password must be at least 8 characters");  
  
export const Name = z  
.string()  
.min(2, "Name must be at least 2 characters");
});
```

```java
// form.common.ts
import { z } from "zod";
import { Email, Password, Name } from "./common.schema";

export const LoginSchema = z.object({
  email: Email,
  password: Password,
});

export const RegisterSchema = z
  .object({
    name: Name,
    email: Email,
    password: Password,
    confirmPassword: z.string(),
  })
  .superRefine((data, ctx) => {
    if (data.password !== data.confirmPassword) {
      ctx.addIssue({
        path: ["confirmPassword"],
        message: "Passwords do not match",
        code: z.ZodIssueCode.custom,
      });
    }
  });

/** ✅ TypeScript Types (IMPORTANT) */
export type LoginFormData = z.infer<typeof LoginSchema>;
export type RegisterFormData = z.infer<typeof RegisterSchema>;
});
```

```typescript
import { useForm, SubmitHandler } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { RegisterSchema, RegisterFormData } from "@/schemas/form.schema";

export default function RegisterForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm<RegisterFormData>({
    resolver: zodResolver(RegisterSchema),
    defaultValues: {
      name: "",
      email: "",
      password: "",
      confirmPassword: "",
    },
  });

  const onSubmit: SubmitHandler<RegisterFormData> = (data) => {
    console.log("Typed Data:", data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name")} placeholder="Name" />
      {errors.name?.message && <p>{errors.name.message}</p>}

      <input {...register("email")} placeholder="Email" />
      {errors.email?.message && <p>{errors.email.message}</p>}

      <input {...register("password")} type="password" />
      {errors.password?.message && <p>{errors.password.message}</p>}

      <input {...register("confirmPassword")} type="password" />
      {errors.confirmPassword?.message && (
        <p>{errors.confirmPassword.message}</p>
      )}

      <button type="submit">Register</button>
    </form>
  );
}
```