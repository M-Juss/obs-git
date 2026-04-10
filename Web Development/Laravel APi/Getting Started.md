Make sure to have this installed to your device:
- php
- composer
- laravel

---

### To Create
1. laravel new name-of-your-choice
2. Starter kit - None
3. Framework - Pest
4. Database - MySQL / SQLite
5. NPM Build - No (since were going to use LARAVEL as API only)
### After Creating moved on to your folder.
-  php artisan serve (runs the server)

---

### Laravel Flow 
**Migration** - Create table in actual Database
- php artisan make:migration sample_table

**Model** - Identifies fields of a subject
- php artisan make:model SampleModel

**Request** - anticipate fields required from the data retrieved in the frontend
- php artisan make:request SampleRequest

**Resource** - Format a specific data an use it to show an organize result
- php artisan make:resource SampleResource

**Factory** - Creates random datas
- php artisan make:factory SampleFactory

**Seed** - Seed the data into the data base
- php artisan make:factory SampleSeed

**Route** - Way for the Frontend and Backend to communicate

---

### Install API Breeze - Contains Sanctum and everything you need  in Laravel API
- php artisan install:api
- keep default installation
- this creates api.php in routes and sanctum and default endpoints

---

### artisan - is a command line tool that gives you ability to perform laravel various task / create, migrate, install and everything
### routes.php
	 - this will define all the routes or endpoints containing functions
	 - Sometimes linked through Controllers
	 - middleware sanctum js simply means accessing endpoint inside it requires authorization and not publicaly accessible

---

### Tinker - execute laravel in terminal and works with the database
 - php artisan tinker
 
#sample-usage
	![[Screenshot 2026-03-30 at 10.26.47 AM.png]]
	-$user-> new User::find();
	 -$user-> new User::where('email' -> 'example@gmail.com') -> first();
	 - $user -> delete();

### Tinker  - a helpful library to do schemas inside the terminal 
User::create(['column' => 'value', 'column' => 'value' 'password' => bcrypt('')]);
User::find(id);
$u = User::find(id);
$u->name = 'updated_value';
$u->save();

---

### Creating Controller 
- php artisan make:controller PostController --api

This will create all of the 5 common function
index() - show all
store() - create one
show() - show specific content
update() - update specific
destroy() - destroy specific 

### In routes it will look like this
Route::get('/post', [PostController::class, 'index'])
Route::post('/post', [PostController::class, 'store'])
Route::get('/post/{id}', [PostController::class, 'show'])
Route::put('/post/{id}', [PostController::class, 'update'])
Route::delete('/post/{id}', [PostController::class, 'destroy'])

### To shortcut all of this use this line instead
`Route::apiResource('/post', PostController::class);`

### Use apiResoure however use specific method only
`Route::apiResource('/post', PostController::class)
	->only(['index', 'store']);`

### Creating a Model with Migration
- php artisan make:model PostModel -m

"-m" means creating a migration. This Migration file creates a schema that will be transferred in the database.

Model ahs 
### Migration 
- Saves all databases scheme changes. 
- up() method all the changes 
- down() method reverted all the changes

---

### Creating a Request class
 - php artisan make:request PostRequest
 This Creates file automatically inside the http
 It's use is to make a clean as seperated file for validating inputs instead of putting it all in the Controllers.
#### message() - this method gives a message when error occurs

### Creating a Resource class
- php artisan make:resource PostResource
Give you ability and control on what you are returning in the API 

```php
class PostResource extends JsonResource{
// public static $wrap = null; this intialization denies the resource 

public function toArray(Request $request): array{

	return [
	"id" => $this->id,
	"title" => $this->title,
	"body" => $this->body,
	"user" => new UserResource($this->user) // this returns format of specfic user in its own format below
  ];
}}

class PostResource extends JsonResource{

// public static $wrap = null;

class UserResource extends JsonResource{

public function toArray(Request $request): array{

	return [
	"id"=> $this->id,
	"name"=> $this->name,
	"email"=> $this->email,
	];
}}
```

### Laravel Breeze -  gives the ability to scaffold the project with authentication into different technologies.
 - composer require laravel/breeze --dev
 - php artisan breeze:install
 -  API Only
 - PEST
 - Yes to migration

---

### 2 Authentication using Sanctum
1. Fully Token-based auth
2. Session & Cookie-based auth
By default Sanctum support all of it. 

---

### How to issue Token? 
- add "HasApiToken" in User Model
- in LoginController initialize createToken in store()
```php
public function store(LoginRequest $request): array{
	$request->authenticate();
	$user = $request->user();
	$token = $user->createToken('auth_token')->plainTextToken;

	return [
	'user' => new UserResource($user),
	'token' => $token,
	];
}
```
- Now in every endpoint put it in the protection of auth:sanctum
```php
Route::middleware('auth:sanctum')->group(function () {
	Route::prefix('v1')->group(function(){
		Route::apiResource('post', V1PostController::class);	
	});
});
```

---

### Rate Limiting - this ensures that the request is safe from spams as it is protected by number of request only

#### Scenario 1 - Group routes with the same rate limiting
```php
Route::middleware(['auth:sanctum', 'throttle:30,1'])->group(function () {
	Route::prefix('v1')->group(function(){
		Route::apiResource('post', V1PostController::class);
	});
	});
```

#### Scenario 2 - Different rate limiting per endpoints
```php
Route::middleware(['auth:sanctum'])->group(function () {
    Route::prefix('v1')->group(function(){
        // Stricter limit for store
        Route::post('post', [V1PostController::class, 'store'])
            ->middleware('throttle:10,1');

        // More relaxed limit for index
        Route::get('post', [V1PostController::class, 'index'])
            ->middleware('throttle:60,1');
    });
});
```

---

### Scenario (Changing Database and Fields)
##### In Backend
- Change columns in Migration
- Change the model fields
- Change the Controller / Requests and methods
##### In Frontend
- Change the validation fields in ZOD
- Change the argument on api method calling