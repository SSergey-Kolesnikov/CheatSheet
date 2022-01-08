[&larr;](readme.md "Laravel") Правила валидации пароля в Laravel Fortify
------------------------------------------------------------------------

Правила валидации пароля в Laravel Fortify описываются в объекте `Laravel\Fortify\Rules\Password` трейта `PasswordValidationRules` файла `/app/Actions/Fortify/PasswordValidationRules.php`. По умолчанию установлено лишь одно правило - это пароль не менее 8 символов. Laravel Fortify позволяет настроить следующие правила валидации пароля:

- `length(<NUMBER>)` - минимальная длинна пароля, где `<NUMBER>` - количество символов;
- `requireUppercase()` - требуется хотя бы один символ верхнего регистра;
- `requireNumeric()` - требуется хотя бы один числовой символ;
- `requireSpecialCharacter()` - требуется хотя бы один специальный символ;

К примеру, если нам необходима минимальная длинна пароля 6 символов, верхний регистр и числа, то в файле `/app/Actions/Fortify/PasswordValidationRules.php` меняем:

```php
    protected function passwordRules()
    {
        return ['required', 'string', new Password, 'confirmed'];

    }
```

на

```php
    protected function passwordRules()
    {
        return [
            'required',
            'string',
            (new Password)
                ->length(6)
                ->requireUppercase()
                ->requireNumeric(),
            'confirmed'
        ];
    }
```

<a name="sources"></a>
## Источники

- [Authentication (jetstream.laravel.com)](https://jetstream.laravel.com/1.x/features/authentication.html#password-validation-rules)
- [How to override the validation rule login Laravel\Fortify? (stackoverflow.com)](https://stackoverflow.com/a/65268872)