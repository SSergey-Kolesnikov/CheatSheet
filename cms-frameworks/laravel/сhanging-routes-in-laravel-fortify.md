[&larr;](readme.md "Laravel") Изменение маршрутов в Laravel Fortify
-------------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Введение](#intro)
- [Маршрут регистрации пользователей](#user-registration-route)
- [Отключение стандартных маршрутов Laravel Fortify](#disabling-standard-laravel-fortify-routes)
- [Изменение формы регистрации](#change-of-registration-form)
- [Заключение](#conclusion)
- [Источники](#sources)

<a name="intro"></a>
## Введение

> Все маршруты Laravel Fortify прописаны в файле `/vendor/laravel/fortify/routes/routes.php`, но редактировать его нельзя, т.к. после каждого запуска Composer'а все изменения в папке `/vendor` будут перезаписаны.

Кастомные маршруты для Laravel Fortify прописываются в файле `/routes/web.php` с посредником (middleware) `fortify`. В данном примере изменим маршрут регистрации пользователей с `/register` на `/registration`.

<a name="user-registration-route"></a>
## Маршрут регистрации пользователей

Прописываем в файле марштрутов `/routes/web.php` необходимый блок (регистрация, авторизация и т.п.) из файла поставщика `/vendor/laravel/fortify/routes/routes.php` и при этом меняем маршрут на необходимый.

```php
...
use Laravel\Fortify\Features;
use Laravel\Fortify\Http\Controllers\RegisteredUserController;
...
Route::group(['middleware' => config('fortify.middleware', ['web'])], function () {
    $enableViews = config('fortify.views', true);

    // Registration...
    if (Features::enabled(Features::registration())) {
        if ($enableViews) {
            Route::get('/registration', [RegisteredUserController::class, 'create'])
                ->middleware(['guest:'.config('fortify.guard')])
                ->name('registration');
        }

        Route::post('/registration', [RegisteredUserController::class, 'store'])
            ->middleware(['guest:'.config('fortify.guard')]);
    }
});
```

<a name="disabling-standard-laravel-fortify-routes"></a>
## Отключение стандартных маршрутов Laravel Fortify

Для отключения стандартных маршрутов Laravel Fortify необходимо в файле `/app/Providers/FortifyServiceProvider.php` в методе `register` прописать `Fortify::ignoreRoutes();`.

```php
    public function register()
    {
        Fortify::ignoreRoutes();
    }
```

> Это отключит все стандартные маршруты Laravel Fortify, поэтому все необходимы маршруты необходимо продублировать из файла `/vendor/laravel/fortify/routes/routes.php` в файл маршрутов `/routes/web.php`.

<a name="change-of-registration-form"></a>
## Изменение формы регистрации

Т.к. маршруты изменились, то необходимо изменить и ссылку на обработчик в файле представления (html-шаблон). Для этого прописываем новый url в файле, к примеру `/resources/views/register.blade.php`.

```html
<form action="/registration" method="POST">
...
</form>
```

<a name="conclusion"></a>
## Заключение

Теперь форма регистрации доступна по url `/registration`, а стандартный url от Laravel Fortify `/register` заблокирован и не работает.

<a name="sources"></a>
## Источники

- [Laravel Fortify (laravel.com)](https://laravel.com/docs/8.x/fortify)
- [Пакет Laravel Fortify (laravel.su)](https://laravel.su/docs/8.x/fortify)
- [Custom Laravel Fortify Routes (youtube.com)](https://www.youtube.com/watch?v=Z3O9Pflsl4g)
- [How do you add a route to Fortify in Laravel 8? (stackoverflow.com)](https://stackoverflow.com/questions/64717650/how-do-you-add-a-route-to-fortify-in-laravel-8?answertab=active#tab-top)
- [Proper way to override Jetstream/Fortify auth routes? (laracasts.com)](https://laracasts.com/discuss/channels/laravel/proper-way-to-override-jetstreamfortify-auth-routes)