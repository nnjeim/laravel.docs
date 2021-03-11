<div class="toolbar">
    <h1>View controllers</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
        <a class="action-link" href="/laravel.docs/views/architecture/web/views">Next</a>
    </div>
</div>

#### Route params
A view controller method is responsible to handle the request object. The Request class instance methods help in collecting
the route params.  
```
//PageController.php

namespace App/Http/Controllers/Web;

use Illuminate\Http\Request;

class PageController
{

    public function viewMethod(Request $request)
    {
        $params = $request->only('page', 'order', 'dir');
        .
        .
        .
        return view('pages.tableView');
    }
}
```

Returning a rendered view can be handled with the view helper method or by initiating the viewFactory class and calling the make method.

```
//PageController.php

namespace App/Http/Controllers/Web;

use Illuminate\View\Factory as ViewFactory;

class PageController
{

 private ViewFactory $viewFactory;

 public function __construct(ViewFactory $viewFactory)
    {
        $this->viewFactory = $viewFactory;
    }
    
    public function viewMethod(Request $request)
    {
        $params = $request->only('page', 'order', 'dir');
        .
        .
        .
        return $this->viewFactory->make('pages.tableView');
    }
}
```

#### The catch all magic

A request for an non existing method is captured by the magic call method and redirected to the private method formView.
The generic blade view `build.blade.php` will be rendered and returned. By passing the variable $method to the builder view, we can load the needded css and js assets.
For instance, by calling a non existing users method we would render the builder blade view and call both the users.js and users.css asset files.
```
namespace App/Http/Controllers/Web;

use Illuminate\Contracts\View\View;
use Illuminate\View\Factory as ViewFactory;

class PageController
{
   
    private ViewFactory $viewFactory;
     
    public function __construct(ViewFactory $viewFactory)
    {
        $this->viewFactory = $viewFactory;
    }

    public function __call(string $method, $args): View
    {
        return $this->formView($method);
    }

    /**
     * @param string $method
     * @return View
     */
    private function formView(string $method): View
    {
        return $this->viewFactory
            ->make('pages.builder', [
                'method' => $method,
            ]);
    }
}
```

#### Reference
<a class="link" href="https://laravel.com/docs/8.x/controllers" target="_blank">Laravel controllers</a>
