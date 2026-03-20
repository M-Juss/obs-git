## Nextjs setup
`pnpm create-next-app@latest --frontend`



## Laravel setup
laravel new api-backend

- mysql
- yes database
- no npm build
-  set databsae in xampp and php myadmiin

### Laravel Code base
- Controller
	- AuthController - > Login, Register, Profile, Logout API
- API 
	- READ, CREATE, UPDATE, DELETE
- Sanctum - authentication 
- api.php
- cors.php

Creating model 
php artisan make:model Product -m 
this one creates model and migration
![[Pasted image 20260320113636.png]]

after that 
php artisan migrate

![[Pasted image 20260320113758.png]]

php artisan install:api

