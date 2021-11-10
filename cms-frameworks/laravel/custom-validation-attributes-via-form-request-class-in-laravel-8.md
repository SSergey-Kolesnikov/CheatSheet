[&larr;](readme.md "Laravel") Кастомные атрибуты валидации через класс запроса формы в Laravel 8
------------------------------------------------------------------------------------------------

## <a name="content"></a> Содержание:

- [Создание класса запроса формы](#create-a-form-request-class)
- [Переопределение метода `attributes`](#overriding-the-attributes-method)
- [Использование в контроллере](#use-in-a-controller)
- [Источники](#sources)

## <a name="create-a-form-request-class"></a> Создание класса запроса формы

```markdown
user@computer:~$ php artisan make:request FormPostRequest
```

В результате выполения команды будет создан файл `/app/Http/Requests/FormPostRequest.php`, включающий два метода - `authorize` и `rules`.

> #### Исходный файл
> 
> ```php
> <?php
> 
> namespace App\Http\Requests;
> 
> use Illuminate\Foundation\Http\FormRequest;
> 
> class FormPostRequest extends FormRequest
> {
>     /**
>      * Determine if the user is authorized to make this request.
>      *
>      * @return bool
>      */
>     public function authorize()
>     {
>         return false;
>     }
> 
>     /**
>      * Get the validation rules that apply to the request.
>      *
>      * @return array
>      */
>     public function rules()
>     {
>         return [
>             //
>         ];
>     }
> }
> 
> ```

## <a name="overriding-the-attributes-method"></a> Переопределение метода `attributes`

Переопределяем метод `attributes` родительского класса `FormRequest` и в нем указываем кастомные атрибуты или переопределяем стандартные из файла `resources/lang/<LANG>/validation.php`, где `<LANG>` - языковая папка.

```php
<?php
...
    /**
     * Get custom attributes for validator errors.
     *
     * @return array
     */
    public function attributes()
    {
        return [
            'email' => 'email address',
        ];
    }
...
```

## <a name="use-in-a-controller"></a> Использование в контроллере

Для примера выбран метод создания записи.

```php
<?php
...
use App\Http\Requests\FormPostRequest;
...
    /**
     * Store a newly created resource in storage.
     *
     * @param  \App\Http\Requests\FormPostRequest  $request
     * @return \Illuminate\Http\Response
     */
    public function store(FormPostRequest $request)
    {
        //
    }
...
```

## <a name="sources"></a> Источники

- [Validation (laravel.com)](https://laravel.com/docs/8.x/validation)
- [Валидация (laravel.su)](https://laravel.su/docs/8.x/validation)
- [FormRequest: валидация форм в Laravel (si-dev.com)](https://si-dev.com/ru/blog/validation-with-formrequest)