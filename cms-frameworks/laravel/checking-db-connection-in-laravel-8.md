[&larr;](readme.md "Laravel") Проверка подключения к БД в Laravel 8
-------------------------------------------------------------------

Из командной строки запускаем Tinker.

```markdown
user@computer:~$ php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.12 — cli) by Justin Hileman
>>> 
```

> Tinker позволяет взаимодействовать полностью со всем приложением Laravel из командной строки, включая модели Eloquent, задачи, события и многое другое.

Далее выполняем код:

```php
try {
    DB::connection()->getPdo();
    if (DB::connection()->getDatabaseName()) {
        echo "Yes! Successfully connected to the DB: " . DB::connection()->getDatabaseName();
    } else {
        die("Could not find the database. Please check your configuration.");
    }
} catch (\Exception $e) {
    die("Could not open connection to database server.  Please check your configuration.");
}
```

И получаем результат об успешном подключении к БД.

```markdown
Yes! Successfully connected to the DB: <DB_NAME>
>>>
```

где:

- `<DB_NAME>` - наименование базы данных;

Общий результат:

```markdown
user@computer:~$ php artisan tinker
Psy Shell v0.10.8 (PHP 7.4.12 — cli) by Justin Hileman
>>> try {
...     DB::connection()->getPdo();
...     if(DB::connection()->getDatabaseName()){
...         echo "Yes! Successfully connected to the DB: " . DB::connection()->getDatabaseName();
...     }else{
...         die("Could not find the database. Please check your configuration.");
...     }
... } catch (\Exception $e) {
...     die("Could not open connection to database server.  Please check your configuration.");
... }
Yes! Successfully connected to the DB: <DB_NAME>
>>>
```

где:

- `<DB_NAME>` - наименование базы данных;

## <a name="sources"></a> Источники

- [Laravel 5.1-проверка подключения к базе данных (askdev.ru)](https://askdev.ru/q/laravel-5-1-proverka-podklyucheniya-k-baze-dannyh-149391/#2)
- [Artisan Console (laravel.com)](https://laravel.com/docs/8.x/artisan)
- [Консоль Artisan (laravel.su)](https://laravel.su/docs/8.x/artisan)