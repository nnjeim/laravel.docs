<div class="toolbar">
    <h1>Web routes</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
        <a class="action-link" href="/laravel.docs/views/architecture/web/viewControllers">Next</a>
    </div>
</div>

Grouped in a the namespace 'Web', all the route requests are directed to the folder web located at:

```
App > Http > Controllers > Web
```
A request is handled by a controller class method which returns a rendered html view.

#### Web route
```
http://laravel.test/users
```
In the web.php route file, we would define the route above as:

```
Route::group(['namespace' => 'Web'], function() {
    Route::get('/users', [RouteController::class, 'viewMethod'])->name('users.index');
});
```

Defining the routes into nested groups is essential to allow the proper scaling of a project.

#### Route nested groups
```
Route::group(['namespace' => 'Web', function() {
    
    ... list of guest routes
    
    Route::group([
        'middleware' => 'auth',
    ], function() { 
        ... list of authenticated routes
    });
});
```

#### Catch all route

Placed at the end of the web routes file, a catch all route definition will be capturing all non defined route requests and routing them to a controller class.

```
Route::get('/{method?}', function ($method = null) {

        $pageController = app()->make(PageController::class);

        if ($method !== null) {
            return $pageController->{$method}();
        }
    });
```
The catch all definition is an appropriate solution when the routing is handled by a Javascript library (Vue or React router). 

#### Reference
<a class="link" href="https://laravel.com/docs/8.x/routing" target="_blank">Laravel routing</a>

