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
// This 
import { z } from "zod";

/** Reusable Fields */
export const Email = z.string().email("Invalid email");
export const Password = z.string().min(8, "Password must be at least 8 chars");


});
```