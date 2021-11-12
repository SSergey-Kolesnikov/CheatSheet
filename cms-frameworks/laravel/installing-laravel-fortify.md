[&larr;](readme.md "Laravel") Установка Laravel Fortify
-------------------------------------------------------

<a name="content"></a>
## Содержание

- [Установка пакета Laravel Fortify](#installing-the-laravel-fortify-package)
- [Публикация ресурсов Laravel Fortify](#publishing-laravel-fortify-resources)
- [Запуск миграций](#running-migrations)
- [Источники](#sources)

<a name="installing-the-laravel-fortify-package"></a>
## Установка пакета Laravel Fortify

Устанавливаем пакет Laravel Fortify через Composer.

```markdown
user@computer:~$ composer require laravel/fortify
Using version ^1.8 for laravel/fortify
./composer.json has been updated
Running composer update laravel/fortify
...
Publishing complete.
```

<a name="publishing-laravel-fortify-resources"></a>
## Публикация ресурсов Laravel Fortify

```markdown
user@computer:~$ php artisan vendor:publish --provider="Laravel\Fortify\FortifyServiceProvider"
Copied File [/vendor/laravel/fortify/stubs/fortify.php] To [/config/fortify.php]
Copied File [/vendor/laravel/fortify/stubs/CreateNewUser.php] To [/app/Actions/Fortify/CreateNewUser.php]
Copied File [/vendor/laravel/fortify/stubs/FortifyServiceProvider.php] To [/app/Providers/FortifyServiceProvider.php]
Copied File [/vendor/laravel/fortify/stubs/PasswordValidationRules.php] To [/app/Actions/Fortify/PasswordValidationRules.php]
Copied File [/vendor/laravel/fortify/stubs/ResetUserPassword.php] To [/app/Actions/Fortify/ResetUserPassword.php]
Copied File [/vendor/laravel/fortify/stubs/UpdateUserProfileInformation.php] To [/app/Actions/Fortify/UpdateUserProfileInformation.php]
Copied File [/vendor/laravel/fortify/stubs/UpdateUserPassword.php] To [/app/Actions/Fortify/UpdateUserPassword.php]
Copied Directory [/vendor/laravel/fortify/database/migrations] To [/database/migrations]
Publishing complete.
```

<a name="running-migrations"></a>
## Запуск миграций

> Перед запуском миграций должно быть настроено подключение к базе данных в файле `/.env`.

```markdown
user@computer:~$ php artisan migrate
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table (44.17ms)
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table (37.61ms)
Migrating: 2014_10_12_200000_add_two_factor_columns_to_users_table
Migrated:  2014_10_12_200000_add_two_factor_columns_to_users_table (39.20ms)
Migrating: 2019_08_19_000000_create_failed_jobs_table
Migrated:  2019_08_19_000000_create_failed_jobs_table (30.72ms)
Migrating: 2019_12_14_000001_create_personal_access_tokens_table
Migrated:  2019_12_14_000001_create_personal_access_tokens_table (42.54ms)
```

<a name="sources"></a>
## Источники

- [Laravel Fortify (laravel.com)](https://laravel.com/docs/8.x/fortify)
- [Пакет Laravel Fortify (laravel.su)](https://laravel.su/docs/8.x/fortify)