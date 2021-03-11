<div class="toolbar">
    <h1>Route controllers</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
        <a class="action-link" href="/laravel.docs/views/architecture/api/requestClasses">Next</a>
    </div>
</div>

### Controllers on diet
A route controller (child ) extends a BaseController abstract class (parent) which:
* Captures the request in a magic call method if the requested method doesn't exist.
* Validates if a request class exists and if it exists the arguments would be captured as:

```
$args = $request->validated(); //array
```

* Forwards the request to an action class which respond with an object containing:
    * A success attribute boolean (true/false).
    * A message attribute.
    * An errors array, empty by default.
    * A data attribute.
    * A meta array if required.
* Responds with a serialized to json object.  


#### Anatomy

1- The child controller should contain two arguments to indicate the path to the request classes and the action classes.

```
namespace App\Http\Controllers\Api\Countries;

use App\Http\Controllers\BaseController;

class CountryController extends BaseController
{
    protected string $requestBasePath = 'App\\Http\\Requests\\Api\\Countries';
    protected string $actionBasePath = 'App\\Actions\\Countries';
}
```

2 - A developer can opt to overwrite all the above by creating a method in the child controller class.

#### Naming convention
With the abstraction done in the BaseController methods the following naming convention should be respected.

<table>
<tbody>
<tr><td>Controller method name</td><td>methodName</td></tr>
<tr><td>Request class name</td><td>MethodNameRequest</td></tr>
<tr><td>Action class name</td><td>MethodNameAction</td></tr>
<tr><td>Action class method name</td><td>execute</td></tr>
</tbody>
</table>


#### Reference
<a class="link" href="https://laravel.com/docs/8.x/controllers" target="_blank">Laravel controllers</a>

