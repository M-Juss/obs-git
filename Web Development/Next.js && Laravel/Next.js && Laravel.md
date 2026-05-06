## Nextjs setup
npx create-next-app@latest --frontend  
npx shadcn@latest init  

npm install zod  
npm install lucide-react  
npm install react-hook-form 
npm install @hookform/resolvers

npx shadcn@latest add button card  
npx shadcn@latest add label input select dialog sonner

npm install @fontsource/inter

## Laravel setup
composer
php

php install
composer install
composer global require laravel/installer

composer require laravel/fortify
composer require laravel/sanctum
php artisan config:publish cors
php artisan install:api

laravel new api-backend

- mysql
- yes database
- no npm build
-  set database in Herd MYSQL WorkBench and HErd![[Screenshot 2026-03-30 at 9.36.20 AM.png]]

Laravel Script CheatSheet
	-  php artisan serve - Runs the server
	- php artisan route:list - show all running routes
	- php artisan migrate:fresh - reset all the schemas inforamtion
	- php artisan make:model ModelName -mcr - this makes a migration, controller, and its registration
### Laravel Code base
- Controller
	- AuthController - > Login, Register, Profile, Logout API
- API 
	- READ, CREATE, UPDATE, DELETE
- Sanctum - authentication 
- api.php![[Screenshot 2026-03-30 at 9.36.20 AM.png]]
- cors.php

Creating model 
php artisan make:model Product -m 
this one creates model and migration
![[Pasted image 20260320113636.png]]

after that 
php artisan migrate![[Screenshot 2026-03-30 at 9.36.20 AM.png]]

![[Pasted image 20260320113758.png]]

php artisan install:api
![[Screenshot 2026-03-30 at 9.36.20 AM.png]]
![[Pasted image 20260320181833.png]]![[Pasted image 20260320182601.png]]![[Screenshot 2026-03-30 at 9.34.02 AM.png]]![[Screenshot 2026-03-30 at 9.36.20 AM.png]]![[Screenshot 2026-03-30 at 9.39.05 AM.png]]![[Pasted image 20260330095749.png]]