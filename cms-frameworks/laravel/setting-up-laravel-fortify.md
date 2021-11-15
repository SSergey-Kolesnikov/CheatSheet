[&larr;](readme.md "Laravel") Настройка Laravel Fortify
-------------------------------------------------------

<a name="content"></a>
## Содержание

- [Регистрация сервис-провайдера Fortify](#registering-a-fortify-service-provider)
- [Настройка Fortify](#setting-up-fortify)
- [Источники](#sources)

<a name="registering-a-fortify-service-provider"></a>
## Регистрация сервис-провайдера Fortify

Для регистрации сервис-провайдера Fortify необходимо открыть файл `/config/app.php` и в конец секции `providers` добавить наш сервис-провайдер:

```php
    'providers' => [

        /*
         * Laravel Framework Service Providers...
         */
        ...
        App\Providers\FortifyServiceProvider::class,

    ],
```

<a name="setting-up-fortify"></a>
## Настройка Fortify

Открываем файл с настройками Fortify `/config/fortify.php` и в массиве `features` все удаляем. В дальнейшем, при подключении авторизации, регистрации и т.п., поочередно можно будет подключать необходимое.

```php
    'features' => [
    ],
```

<a name="sources"></a>
## Источники

- [Laravel Fortify (laravel.com)](https://laravel.com/docs/8.x/fortify)
- [Пакет Laravel Fortify (laravel.su)](https://laravel.su/docs/8.x/fortify)
- [Меняем Laravel UI на Laravel Fortify (laravel.demiart.ru)](https://laravel.demiart.ru/changing-laravel-iu-to-laravel-fortify/)
- [Laravel 8 authentication with Bootstrap and Fortify (dev.to)](https://dev.to/jasminetracey/laravel-8-with-bootstrap-livewire-and-fortify-5d33)