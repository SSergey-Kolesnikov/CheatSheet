[&larr;](readme.md "Laravel") Авторизация через Laravel Fortify
---------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Создание шаблонов](#creating-templates)
    - [Создание шаблона-болванки под страницы](#creating-a-blank-template-for-pages)
    - [Создание шаблона страницы авторизации](#creating-a-login-page-template)
- [Обновление провайдера Fortify](#fortify-provider-update)
- [Защита маршрутов](#route-protection)
- [Редирект после авторизации](#redirect-after-authorization)
- [Источники](#sources)

<a name="creating-templates"></a>
## Создание шаблонов

<a name="creating-a-blank-template-for-pages"></a>
### Создание шаблона-болванки под страницы

Создаем файл `/resources/views/layouts/app.blade.php` под шаблон-болванку и добавляем в него следующее содержимое:

```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>@yield('title')</title>
    <link rel="stylesheet" href="{{ URL::asset('css/bootstrap.min.css') }}" type="text/css" />
</head>
<body>
@yield('body')
<script type="text/javascript" src="{{ URL::asset('js/bootstrap.min.js') }}"></script>
</body>
</html>
```

Так же, по указанным в файле путям, добавляем стили и скрипты Bootstrap'а.

<a name="creating-a-login-page-template"></a>
### Создание шаблона страницы авторизации

Создаем файл `/resources/views/login.blade.php` под страницу авторизации и добавляем в него следующее содержимое:

```html
@extends('layouts.app')
@section('title', 'Авторизация')
@section('body')
    <main class="registration-form">
        <div class="container">
            <div class="row">
                <form action="{{ route('login') }}" method="POST">
                    {!! csrf_field() !!}

                    <h1 class="h3 mb-3 text-center">Авторизация</h1>

                    <div class="mb-3">
                        <label for="email">Email</label>
                        <input type="email" name="email" value="{{ old('email') }}" class="form-control @error('email') is-invalid @enderror" id="email">
                        @error('email')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>

                    <div class="mb-3">
                        <label for="password">Пароль</label>
                        <input type="password" name="password" value="{{ old('password') }}" class="form-control @error('password') is-invalid @enderror" id="password">
                        @error('password')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>

                    <button type="submit" class="w-100 btn btn-lg btn-primary">Авторизоваться</button>
                </form>
            </div>
        </div>
    </main>
@endsection
```

<a name="fortify-provider-update"></a>
## Обновление провайдера Fortify

Для Fortify необходимо указать, где именно находятся шаблоны аутентификации. В файле `/app/Providers/FortifyServiceProvider` необходимо обновить метод `boot`, дописываем в конец метода:

```php
    public function boot()
    {
        ...
        Fortify::loginView(function () {
            return view('login');
        });
    }
```

<a name="route-protection"></a>
## Защита маршрутов

Для защиты маршрутов открываем файл `/routes/web.php` и, к примеру маршруты админ. панели, оборачиваем посредником (middleware).

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::prefix('/admin')->group(function () {
        ...
    });
});
```

<a name="redirect-after-authorization"></a>
## Редирект после авторизации

По умолчанию Laravel Fortify редиректит на `/home`, но если такой страницы нет, то необходимо перенастроить редирект на имеющуюся. Для этого в файле `/config/fortify.php` и в ключе `home` указываем необходимый url, куда будет перенаправляться пользователь после авторизации.

Меняем:

```php
    'home' => RouteServiceProvider::HOME,
```

на:

```php
    'home' => '<URL>',
```

где:

- `<URL>` - url страницы для редиректа пользователя после авторизации;

Если необходимо сделать редирект на главную страницу, то не обязательно менять `'home' => RouteServiceProvider::HOME,` на ` 'home' => '/',`, а можно переопределить константу `RouteServiceProvider::HOME`, которая используется аутентификацией Laravel для перенаправления пользователей после входа в систему. Для этого переходим в файл `/app/Providers/RouteServiceProvider.php` и меняем константу `HOME` с:

```php
    public const HOME = '/home';
```

на:

```php
    public const HOME = '/';
```

<a name="sources"></a>
## Источники

- [Laravel Fortify (laravel.com)](https://laravel.com/docs/8.x/fortify)
- [Пакет Laravel Fortify (laravel.su)](https://laravel.su/docs/8.x/fortify)
- [Меняем Laravel UI на Laravel Fortify (laravel.demiart.ru)](https://laravel.demiart.ru/changing-laravel-iu-to-laravel-fortify/)
- [Laravel 8 authentication with Bootstrap and Fortify (dev.to)](https://dev.to/jasminetracey/laravel-8-with-bootstrap-livewire-and-fortify-5d33)
- [Redirect after login according to user role laravel fortify (laracasts.com)](https://laracasts.com/discuss/channels/laravel/redirect-after-login-according-to-user-role-laravel-fortify)