# `REST API` BASIC STEP IN `LARAVEL 8`
## STEP 0: CREATE NEW PROJECT 
> `composer create-project laravel/laravel project-name --prefer-dist`

#### OR

> `composer global require laravel/installer`

> `laravel new project-name`

## STEP 1: CREATE MODEL AND TABLE
> `php artisan make:model Sample  -m`

## STEP 2: ADD COLUMN TO TABLE
- database/migration/
- add column to table 

**Example:** 
>$table->id(); <br>
> $table->string('title'); <br>
> $table->string('description'); <br>
>$table->timestamps();
## STEP 3: ALLOW COLUMN IN MODEL 
> protected $fillable = ['column 1', 'column 2', 'column 3'...];

## STEP 4: MIGRATE YOUR TABLE TO DATABASE
> `php artisan migrate`

## STEP 5: CREATE CONTROLLER API 
> `php artisan make:controller SampleController  --api`

## STEP 6: CRUD API BASIC
> use App\Models\Sample;

### index() `function`
>public function index() { <br> 
> return Sample::all(); <br>
>}

### store() `function`
>public function store(Requst $request) { <br>
> return Sample::create($request->all()); <br>
>}

### show() `function`
> public function show($id) { <br>
> return Sample::find($id); <br>
> }

### update() `function`
> public function update(Request $requst, $id) { <br>
> $obj = Sample::find($id); <br>
> $obj->update($request->all()); <br>
> return $obj; <br>
>}

### destroy() `function`
> publi function destroy($id) { <br>
> return Sample::destroy($id); <br>
>}

## STEP 7: CREATE ROUTE WITH CONTROLLER
Go to routes/api.php

> use App\Http\Controllers\SampleController;

### `GET ALL`
> Route::get('/samples', [SampleController::class, 'index']);
### `GET ONE`
> Route::get('/samples/{id}', [SampleController::class, 'show']);
### `CREATE`
> Route::post('/samples', [SampleController::class, 'store']);
### `UPDATE`
> Route::put('/samples/{id}', [SampleController::class, 'update']);
### `DELETE`
> Route::delete('/samples/{id}', [SampleController::class, 'destroy']);

## STEP 8: TEST CRUD API 
You can use any tools to test api example:
- Postman
- Thunder Client (VScode extension)
> `GET | POST | PUT | DELETE`

## STEP 9: CREATE RESOURCE API 
> `php artisan mak:resource SampleResource`

- Check : App/Http/Resources folder
- Open SampleResource.php (file that we just created)
- In function `toArray($request)` delete return and add new code

**Example**
> return [ <br>
>   'title' => $this->title, <br>
>   'description' => $this->description, <br>
>];

## STEP 10: USE API RESOURCE IN CONTROLLER
In SampleController, you can use:
> use App\Http\Resources\SampleResource;

We will use resource in 2 functions is `index()` && `show()`

> index(): SampleResource::collection(Sample::all());

> show($id): new SampleResource(Sample::find($id));

## STEP 11: CREATE SEEDER && USE FAKER LIBRARY
> `php artisan make:seeder SampleSeeder`

- In `database/seeders`
- Open `SampleSeeder` file and use
> use Illuminate\Support\Facades\DB; <br>
> use Faker\Factory as Faker;

In function `run()` so lets start to insert data ramdomly

**Example**
> $faker = Faker::create(); <br>
> DB::table('samples')->insert([ <br>
> 'title' => $faker->sentence(), <br>
> 'description' => $faker->paragraph() <br>
>]);

## STEP 12: CALL SampleSeeder TO `DatabaseSeeder`
Open `DatabaseSeeder.php` in function `run()`

> $this->call([ <br>
> SampleSeeder::class, <br>
>]);

### `Then`

> `php artisan db:seed`

**Noted:** `If it doesn't work you need to type this command first:`

> `composer dump-autoload`

----------------------------------------------------------------
### `@copyright by Rady Y` documentation v1.0
----------------------------------------------------------------
