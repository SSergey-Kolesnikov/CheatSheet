[&larr;](readme.md "Laravel") Регистрация через Laravel Fortify
--------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Создание шаблонов](#creating-templates)
    - [Создание шаблона-болванки под страницы](#creating-a-blank-template-for-pages)
    - [Создание шаблона страницы регистрации](#creating-a-registration-page-template)
- [Настройка Fortify](#setting-up-fortify)
- [Обновление провайдера Fortify](#fortify-provider-update)
- [Редирект после регистрации](#redirect-after-registration)
- [Заключение](#conclusion)
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

<a name="creating-a-registration-page-template"></a>
### Создание шаблона страницы регистрации

Создаем файл `/resources/views/register.blade.php` под страницу регистрации и добавляем в него следующее содержимое:

```html
@extends('layouts.app')
@section('title', 'Регистрация')
@section('body')
    <main class="register-form">
        <div class="container">
            <div class="row">
                <form action="/register" method="POST">
                    {!! csrf_field() !!}

                    <h1 class="h3 mb-3 text-center">Регистрация</h1>

                    <div class="mb-3">
                        <label for="name">Имя</label>
                        <input type="text" name="name" value="{{ old('name') }}" class="form-control @error('name') is-invalid @enderror" id="name">
                        @error('name')
                            <div class="invalid-feedback">{{ $message }}</div>
                        @enderror
                    </div>

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

                    <div class="mb-3">
                        <label for="password-confirmation">Подтверждение пароля</label>
                        <input type="password" name="password_confirmation" class="form-control" id="password-confirmation">
                    </div>

                    <button type="submit" class="w-100 btn btn-lg btn-primary">Зарегистрироваться</button>
                </form>
            </div>
        </div>
    </main>
@endsection
```

<a name="setting-up-fortify"></a>
## Настройка Fortify

Открываем файл с настройками Fortify `/config/fortify.php` и в массив `features` добавляем функцию регистрации.

```php
    'features' => [
        ...
        Features::registration(),
        ...
    ],
```

<a name="fortify-provider-update"></a>
## Обновление провайдера Fortify

Для Fortify необходимо указать, где именно находятся шаблоны аутентификации. В файле `/app/Providers/FortifyServiceProvider` необходимо обновить метод `boot`, дописываем в конец метода:

```php
    public function boot()
    {
        ...
        Fortify::registerView(function () {
            return view('register');
        });
    }
```

<a name="redirect-after-registration"></a>
## Редирект после регистрации

По умолчанию Laravel Fortify редиректит на `/home`, но если такой страницы нет, то необходимо перенастроить редирект на имеющуюся. Для этого в файле `/config/fortify.php` и в ключе `home` указываем необходимый url, куда будет перенаправляться пользователь после регистрации.

Меняем:

```php
    'home' => RouteServiceProvider::HOME,
```

на:

```php
    'home' => '<URL>',
```

где:

- `<URL>` - url страницы для редиректа пользователя после регистрации;

Если необходимо сделать редирект на главную страницу, то не обязательно менять `'home' => RouteServiceProvider::HOME,` на ` 'home' => '/',`, а можно переопределить константу `RouteServiceProvider::HOME`, которая используется аутентификацией Laravel для перенаправления пользователей после входа в систему. Для этого переходим в файл `/app/Providers/RouteServiceProvider.php` и меняем константу `HOME` с:

```php
    public const HOME = '/home';
```

на:

```php
    public const HOME = '/';
```

<a name="conclusion"></a>
## Заключение

После успешного заполнения формы регистрации со страницы `/register` пользователь будет сразу авторизован, это необходимо учитывать.

<a name="sources"></a>
## Источники

- [Laravel Fortify (laravel.com)](https://laravel.com/docs/8.x/fortify)
- [Пакет Laravel Fortify (laravel.su)](https://laravel.su/docs/8.x/fortify)
- [Меняем Laravel UI на Laravel Fortify (laravel.demiart.ru)](https://laravel.demiart.ru/changing-laravel-iu-to-laravel-fortify/)
- [Laravel 8 authentication with Bootstrap and Fortify (dev.to)](https://dev.to/jasminetracey/laravel-8-with-bootstrap-livewire-and-fortify-5d33)