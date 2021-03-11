<div class="toolbar">
    <h1>Single method actions</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
    </div>
</div>


### Action class
The action benefits from a single public method named 'execute'.  
The method 'execute' accept one argument which can be:
* An array of arguments that can be destructured as:


  ```
  public function execute(array $args) {
    list(
        'id' => $id,
        'name' => $name,
    ) = $args;
    .
    .
    .
  }
  ```
* A request instance could be also used as a single argument which potentially combines:
    * A file raw data in case the action is used to upload.
    * And the validated arguments coming from the request class.


    ```
    public function execute(Request $request) {
        list(
            'id' => $id,
            'name' => $name,
        ) = $request->validated();
        
        //File raw data: $request->file('originalFileName'); 
        .
        .
        .
    }
    ```
* The action class is responsible to:
    * Process the business logic as DB queries, Api calls ...
    * Cache the data;
    * Transform the data with a transformer class
    * Event
    * ... etc.
* Format the response back to the BaseController.


```
  /**
  * @param array $data
  * @return $this
  */
  private function formResponse(array $data): self
  {
  $this->success = true;
  
          $this->data = $data;
  
          return $this;
      }
```
