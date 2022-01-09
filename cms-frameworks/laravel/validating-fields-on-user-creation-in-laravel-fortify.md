[&larr;](readme.md "Laravel") Валидация полей при создании пользователя в Laravel Fortify
-----------------------------------------------------------------------------------------

Валидация полей при создании пользователя в Laravel Fortify происходит в методе `make` фасада `Validator` в файле `/app/Actions/Fortify/CreateNewUser.php`. В метод `make` передаем все необходимые правила:

```php
        Validator::make($input, [
            'name' => ['required', 'string', 'max:255'],
            'email' => [
                'required',
                'string',
                'email',
                'max:255',
                Rule::unique(User::class),
            ],
            'password' => $this->passwordRules(),
        ])->validate();
```

<a name="sources"></a>
## Источники

- [Validation (laravel.com)](https://laravel.com/docs/8.x/validation)
- [Валидация (laravel.su)](https://laravel.su/docs/8.x/validation)
- [How to override the validation rule login Laravel\Fortify? (stackoverflow.com)](https://stackoverflow.com/a/65268872)
- [fortify/CreateNewUser.php at laravel/fortify (github.com)](https://github.com/laravel/fortify/blob/master/stubs/CreateNewUser.php#L21)