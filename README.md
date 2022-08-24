# Awesome Laravel Interview questions

Get well-prepared for your next Laravel career! 


## Languages
- English (this)
- ...

## Table of Contents


### Basic

1. Migrations & Seeders
2. Routing
3. Middlewares
4. Requests
5. Controllers
6. Models / Eloquents / Query Builders
7. Responses

### Deep-dive

1. Service Provider
2. Service Container
3. Facade
4. Artisan Commands
5. Queue
6. Events / Listeners
7. Task Scheduling - Cron Job
8. Test
    1. Unit tests
    2. Feature tests

## Basic Questions

### 1/ Migrations & Seeders

1. Use cases of Migrations & Seeders?
    - Use `Migrations` for actions that affecting table's structure (CREATE, ALTER, DROP)
    - Use `Seeders` for actions that affecting table's data (INSERT, UPDATE, DELETE)
2. When creating a Migration to create a table, what are the recommendations for the new table?
    - Use the default `timestamps()` method to create `created_at` and `updated_at` which built-in in Eloquent, helps to track
    - Use the `softDeletes()`, avoid hard-delete on the Production - data is king.
3. Can I put multiple statements in a same Migration?
    - No, avoid to do so. We never know if a Migration went wrong, once it goes wrong, we can't hit the `migrate` command again because there would be some statement that already ran in the previous migration.
    - Keep the Migration as small as possible.
4. Which helpers that I can use for Seeders?
    - Faker
    - Factory

### 2/ Routing

1. Best practices of Laravel's Routes?
    - Using kebab-case for the route (eg: `my-details`, `user-details/profile`,...)
    - Follow this register `Route::get('my-details', [MyDetailsController::class, 'index'])`;
    - Group the same prefix routes
2. What is the main benefit of the `Route::resource(..)`?
    - To register CRUD routes in 1 line only
3. How to optimize the routes computing times?
    - By caching it, using `php artisan route:cache`

### 3/ Middlewares

1. Pros and Cons of `protected $middleware`?
    - Pros: my middleware will be triggered for every requests
    - Cons: I can't access to sessions or cookies because it will be computed in a later Middlewares (`web` group)
2. Usage of `throttle`?
    - 2 params: first one is the number of requests, second one is the allowance time. Eg: `throttle:300,1` means 300 requests in 1 minute
3. We can handle things before the request is going to Controller, but can we handle something after the process of Controller finished?
    - Yes, basically we can invoke `$next($request)` and the line below, we can add our custom actions

Coming soon...

## Deep-dive Questions

Coming soon...

## Contributions
- Seth Phat
- ...
