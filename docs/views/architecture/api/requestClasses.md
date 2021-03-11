<div class="toolbar">
    <h1>Request classes</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
        <a class="action-link" href="/laravel.docs/views/architecture/api/singleMethodActions">Next</a>
    </div>
</div>

#### Anatomy

A request class extends the BaseRequest class. 
It contains a single method named `rules` which returns an array containing the request parameters to be validated and the correspondant validation rule.
A long list of validation rules is to be explored in the Laravel official documentation.

```
namespace App\Http\Requests\Api\Countries;

use App\Http\Requests\BaseRequest;

class IndexRequest extends BaseRequest
{
    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'cities' => 'sometimes|required|boolean',
        ];
    }
}

```

```
//App/Http/Requests/BaseRequest.php

namespace App\Http\Requests\Api;

use Illuminate\Contracts\Validation\Validator;
use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Http\Exceptions\HttpResponseException;

class BaseRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize()
    {
        return true;
    }

    /**
     * @param  Validator  $validator
     */
    protected function failedValidation(Validator $validator)
    {
        throw new HttpResponseException(response()->json([
            'success' => false,
            'errors' => $validator->errors(),
        ], 422));
    }
}

```

#### Authorization
The base request class contains the method `authorize` which controls if the request can go thru or will be rejected. This method should only return a bool.

#### Http exception
A failed validation should throw an error in a form of a json object with a 422 status code. 
The failedValidation method is responsible to throw the Http exception.

#### Request object alteration

The request object can be programatically altered by adding the validated method in the request class.

```
 public function validated()
    {
        return array_merge(parent::validated(), [
            'my_field' => 'my_value',
        ]);
    }
```

#### Reference
<a class="link" href="https://laravel.com/docs/8.x/validation" target="_blank">Laravel validation</a>

