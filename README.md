# Awesome Laravel Interview questions

Get well-prepared for your next Laravel career and push your Laravel knowledge to a new level, super advanced! 

This will focus on **100% backend questions** based on Laravel framework. 

## Languages
- English (this)
- Vietnamese (coming soon)
- ...

## Other Recommendations
- [PHP interview questions](https://github.com/DopplerHQ/awesome-interview-questions#php)
- [Database interview questions](https://github.com/DopplerHQ/awesome-interview-questions#database-technologies)
    - Main focus: MySQL/MariaDB or PostgreSQL
- [System Designs](https://github.com/donnemartin/system-design-primer)

## Table of Contents


### Basic

1. [Migrations & Seeders](https://github.com/sethsandaru/awesome-laravel-interviews#1-migrations--seeders)
2. [Routing](https://github.com/sethsandaru/awesome-laravel-interviews#2-routing)
3. [Middlewares](https://github.com/sethsandaru/awesome-laravel-interviews#3-middlewares)
4. [Requests](https://github.com/sethsandaru/awesome-laravel-interviews/blob/main/README.md#4-requests)
5. [Controllers](https://github.com/sethsandaru/awesome-laravel-interviews#5-controllers)
6. [Models / Eloquents / Query Builders](https://github.com/sethsandaru/awesome-laravel-interviews#6-models--eloquents--query-builders)

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

1. Pros and Cons of registering your custom middleware in `protected $middleware`?
    - Pros: my middleware will be triggered for every requests
    - Cons: I can't access to sessions or cookies because it will be computed in a later Middlewares (`web` group)
2. Usage of `throttle`?
    - `throttle:300,1` means we only allow **300 requests** in **1 minute**
    - Use it to avoid spaming/hijacking requests
3. We can handle things before the request is going to Controller, but can we handle something after the process of Controller finished?
    - Yes, basically we can invoke `$next($request)` and the line below, we can add our custom actions
    ```php
    // Sample Code
    public function handle(Request $request, Closure $next) {
        $result = $next($request);
        // do your own logic here
        Log::info('Request log:' . json_encode($result));
        
        return $result;
    }
    ```

### 4/ Requests

1. Do you use custom FormRequest? What are the benefis of using FormRequest.
    - A single place to validate the request: authorization & data validation before going to Controller to be processed.
    - Request can only reach to the Controller once everything is validated
2. How can I perform some actions after the authorization check or validation check?
    - Use `passedAuthorization()` and `passedValidation()` hooks to achieve that.
3. What can I do more for my custom FormRequest class?
    - You can implement `getter` methods eg `getAccount()`, `getTopic()` and make them return the **exact type**, so from your Controller to can retrieve the needful typed instances. A great help for IDE as well.

### 5/ Controllers

1. Best practices of Controller?
    - Use FormRequest to validate all of the data, then from Controller, we can start the processing without any checking.
    - Prefer Dependency Injection (ideally in the method's parameters)
    - If there are too much things to handle, create multiple services to handle instead of putting all logic in 1 place
    - Always prepare the return type of Controller's methods (JsonResponse, ViewResponse,...)
    - Follows Laravel's Resource structure (index, show, create, update,...)
2. How I can invoke another Controller's method?
    - You don't, and it is super bad practice. You need to extract the login into a Service, then inject the Service where you want to use.
    - Following DRY - Don't repeat yourself
3. Can I register my Controller without any methods in the `routes` file?
    - You can, then you need to implement the `__invoke()` method in order to make it work.
    
### 6. Models / Eloquents / Query Builders

1. How to avoid N+1 problems?
    - By using eager-loading. 
2. How to trace queries of Eloquents / Query Builders?
    - You can use Laravel Debugbar, Ray, Telescope,...
    - For PROD applications, you can use DataDog, BlackFire,...
3. How to know which fields/columns that a single Eloquent Model has?
    - We need to manually add the phpDoc and maintain the @property there. And it is IDE-friendly.

Continue....

## Deep-dive Questions

Coming soon...

## Contributions
- Seth Phat
- ...
