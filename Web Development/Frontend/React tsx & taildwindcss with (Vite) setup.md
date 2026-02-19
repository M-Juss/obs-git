## Step-by-Step Setup

### 1. Create a New React + TypeScript Project with Vite

1. Open **VSCode** and open the terminal (select **PowerShell**).
    
2. Run the command:
    
    `npm create vite@latest project_name`
    
3. During setup:
    
    - Select **React** framework
        
    - Select **TypeScript** variant
        
    - Select **No** for Rollup + Vite options
        
    - Select **Yes** to install npm dependencies
        

---

### 2. Install Tailwind CSS in Vite

1. Navigate to your project directory:
    
    `cd project_name`
    
2. Install Tailwind CSS:
    
    `npm install tailwindcss @tailwindcss/vite`
    

---

### 3. Setup Tailwind CSS in Your Project

1. Open `vite.config.ts` and paste the following:

```tsx
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```

2. Open `index.css`, remove everything, and paste:
    @import "tailwindcss";

---

### 4. Add Theme and Base Styles

1. In the same `index.css`, add:
```tsx
@theme {
  --font-display: "Poppins", "sans-serif";
  --color-primary: #1DA1F2;
  --color-secondary: #14171A;
  --color-accent: #657786;
}

@layer base {
  body {
    font-family: var(--font-display);
    background-color: var(--color-secondary);
    color: white;
    margin: 0;
    padding: 0;
  }
}
```

### 5. Delete Default App Styles
1. Remove `App.css` from the `src` folder.

✅ **You’re good to go!** Now you can start building your website with React, TypeScript, and Tailwind CSS by customizing your App.tsx



