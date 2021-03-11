<div class="toolbar">
    <h1>Api routes</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
        <a class="action-link" href="/laravel.docs/views/architecture/api/routeControllers">Next</a>
    </div>
</div>

<p class="mx-auto fit-content p-3"><img src="/laravel.docs/images/singleAction.svg" height="120"/></p>

Grouped in a the namespace 'Api', all the api requests are directed to the folder api located at:

```
App > Http > Controllers > Api
```

In the api.php route file, we would define a route as:

```
Route::group(['namespace' => 'Api'], function() {
    Route::get('/paginate', [RouteController::class, 'viewMethod']);
});
```

Defining the routes into nested groups is essential to allow the proper scaling of a project.

#### Nested groups

```
Route::group(['namespace' => 'Api', function() {
     
     ... non authenticated routes
        
     Route::group([
        'middleware' => 'auth',
    ], function() { 
        ... list of authenticated routes
    
        Route::group([
            'middleware' => 'custom.middleware',
            'prefix' => 'users',
            'as' => 'users',
        ], function() { 
            
            Route::get('/', [UsersController::class, 'index'])->name('index');
            
            Route::get('/paginate', [UsersController::class, 'paginate'])->name('paginate');
        });
    });
    
    .
    .
    .
});
```

#### Reference
<a class="link" href="https://laravel.com/docs/8.x/routing" target="_blank">Laravel routing</a>

