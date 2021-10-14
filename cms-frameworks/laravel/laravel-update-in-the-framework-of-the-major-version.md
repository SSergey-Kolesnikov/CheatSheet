[&larr;](readme.md "Laravel") Обновление Laravel в рамках мажорной версии
-------------------------------------------------------------------------

Инструкция по обновлению фреймворка Laravel за 8 шагов в рамках мажорной версии. По данной инструкции был обновлен Laravel с версии 8.47.0 до версии 8.64.0.

## <a name="content"></a> Содержание:

- [Бекап проекта](#project-backup)
- [Обновление файла `composer.json`](#updating-the-composer-json-file)
- [Удаляем файл `composer.lock`](#delete-the-composer-lock-file)
- [Очищаем кеш Composer](#clearing-the-composer-cache)
- [Очищаем кеша Laravel](#clearing-the-laravel-cache)
- [Удаляем папку `/vendor`](#delete-the-folder-vendor)
- [Устанавливаем Laravel и пакеты через Composer](#installing-laravel-and-packages-via-composer)
- [Проверяем версию Laravel](#checking-the-laravel-version)
- [Заключение](#conclusion)
- [Источники](#sources)

## <a name="project-backup"></a> Бекап проекта [&uarr;](#content "Содержание")

Необходимо сделать полный бекап, который включает все файлы проекта.

## <a name="updating-the-composer-json-file"></a> Обновление файла `composer.json` [&uarr;](#content "Содержание")

С официального репозитория [Laravel](https://github.com/laravel/laravel) скачиваем актуальный файл `composer.json` и дополняем его сторонними пакетами из текущего файла `composer.json`. Это необходимо для сохранения и обновления сторонних пакетов, которые были дополнительно установлены для проекта. Для сравнения файлов `composer.json` можно использовать специальные программы сравнения, а правки внести "руками".

> Composer поддерживает некоторые макросы и вместо указания версии можно указать макрос `@stable`, благодаря которому каждое обновление будет вытягивать последние стабильные версии библиотек.

В моем случае были установлены две дополнительные библиотеки, это [laravel/fortify](https://github.com/laravel/fortify) и [barryvdh/laravel-debugbar](https://github.com/barryvdh/laravel-debugbar) + пакет [fideloper/proxy](https://github.com/fideloper/TrustedProxy) от предыдущей версии Laravel. Поэтому в файле `composer.json` добавляем информацию по ним с макросом `@stable`.

```markdown
{
    ...
    "require": {
        ...
        "fideloper/proxy": "@stable",
        ...
        "laravel/fortify": "@stable",
        ...
    },
    "require-dev": {
        "barryvdh/laravel-debugbar": "@stable"
        ...
    },
    ...
}
```

## <a name="delete-the-composer-lock-file"></a> Удаляем файл `composer.lock` [&uarr;](#content "Содержание")

В файле `composer.lock` хранится информация о текущих установленных версиях пакетов и чтобы не возникало конфликтов при обновлении Laravel, удаляем этот файл.

## <a name="clearing-the-composer-cache"></a> Очищаем кеш Composer [&uarr;](#content "Содержание")

Данный шаг необходим для получения актуальных версий пакетов, которые указаны в файле `composer.json`. Если не очистить кеш, то пакеты будут ставиться из кеша Composer, а не скачиваться.

```markdown
user@computer:~$ composer clearcache
Cache directory does not exist (cache-vcs-dir): 
Clearing cache (cache-repo-dir): /home/user/.cache/composer/repo
Clearing cache (cache-files-dir): /home/user/.cache/composer/files
Clearing cache (cache-dir): /home/user/.cache/composer
All caches cleared.
```

## <a name="clearing-the-laravel-cache"></a> Очищаем кеш Laravel [&uarr;](#content "Содержание")

Очищаем кеш самого фреймворка от данных, которые могли быть созданы с использованием устаревших пакетов.

```markdown
user@computer:~$ php artisan optimize:clear
Compiled views cleared!
Application cache cleared!
Route cache cleared!
Configuration cache cleared!
Compiled services and packages files removed!
Caches cleared successfully!
```

Дополнительно проходимся по директориям, вложенных в `/storage/framework`, и удаляем вручную все файлы, кроме `.gitignore`.

## <a name="delete-the-folder-vendor"></a> Удаляем папку `/vendor` [&uarr;](#content "Содержание")

В каталоге `/vendor` хранятся все Composer-зависимости, удаляем эту папку. Все Composer-зависимости будут скачаны и установлены повторно после запуска команды `composer install`.

## <a name="installing-laravel-and-packages-via-composer"></a> Устанавливаем Laravel и пакеты через Composer [&uarr;](#content "Содержание")

```markdown
user@computer:~$ composer install
No lock file found. Updating dependencies instead of installing from lock file. Use composer update over composer install if you do not have a lock file.
Loading composer repositories with package information
Updating dependencies
...
> @php artisan vendor:publish --tag=laravel-assets --ansi
No publishable resources for tag [laravel-assets].
Publishing complete.
```

## <a name="checking-the-laravel-version"></a> Проверяем версию Laravel [&uarr;](#content "Содержание")

```markdown
user@computer:~$ php artisan --version
Laravel Framework 8.64.0
```

## <a name="conclusion"></a> Заключение [&uarr;](#content "Содержание")

На этом все, Laravel был обновлен до последней актуальной версии.

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [Laravel update: обновляем движок за 8 шагов (cccp-blog.com)](http://cccp-blog.com/laravel/laravel-update#instruktsiya-po-laravel-update)
- [Как обновить библиотеки в файле composer.json до актуальных версий (evilinside.ru)](https://evilinside.ru/kak-obnovit-biblioteki-v-fajle-composer-json-do-aktualnyx-versij/)