 pnpm create-next-app@latest
 - use typescript
 - use ESlint
 - use Tailwind
 - use src/directory
 - use App Router (folder routing)
 - use turbo pack (for speed of the app)
 -  Forimporting alises use default

## Understanding Folder Structure
- tsconfig.json - every package in typescript
- postcss.config.mjs - the use tailwind
- package.json - scripts / paclage u need to run the application (next build is prepairing your app to productio. next start to start it in production)
- next.config.json - packages of configuration 
- eslint.config.jspn - packages of eslint
- .gitignore - .env and something what wont be included when pushing into repo
- public - public acessible from the client / users. Images should be here
- .next - generated on build for cache files
- app 
	- favicon.ico this is the thumbnail in the new tab feel free to change it but not the name
	- global css - these s where you put themes, global structure and designs
	- layout.tsx - where you build html structure. calling every page as its children. Cool thing is that when you put code outside the children. It will render it in each page. Like a global and static styling for each page.
	- page.tsx - this is the default page or home of the app.

## Setting up routing and navigation
- File based routing - Where in the Folder will be its route and inside the folder will be its page.tsx
- Using <Link/> -Link tag is same as the a tag syntax: <Link href={/contact}> `<Link href={/router}>Contact </Link>`


## Working with image 
- Image component <Image/> - Fast and optimize compared to <`img/`> it has different attributes for being responsive on screen dimension and fast loading.
	- attributes common
		 - classname=""
		 - src=""
		 - alt=""
		 - width=""
		 - height=""
		 - priority
	- When exporting images from external resources 
		- go to next.config to allow and specify it. 
		

![[Screenshot 2026-03-14 at 11.14.10 AM.png]]

## Server vs Client Components
- ## 1️⃣ Server Components (in Next.js)

**Key idea:** They run **only on the server**, not in the browser.

**Characteristics:**

- ❌ No user interaction (no `onClick`, `useState`, `useEffect`)
    
- ⚡ Faster initial load
    
- 🔍 Better for SEO because HTML is generated on the server
    
- 📦 Smaller JavaScript bundle sent to the browser

## 2️⃣ Client Components

**Key idea:** They run **in the browser** and allow **interaction**.

They must include:

"use client"

**Characteristics:**

- ✅ Supports user interaction (`onClick`, forms)
    
- ✅ Can use hooks (`useState`, `useEffect`)
    
- ❌ More JavaScript sent to the browser
    
- ❌ Slightly slower initial load compared to server components


## Pre-defined files that can be reuse and customize
## not-found.tsx
## Loading.tsx
## error.tsx
