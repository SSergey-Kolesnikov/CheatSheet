[&larr;](readme.md "1С-Битрикс") Авторизация в админ. панели Битрикса без пароля
--------------------------------------------------------------------------------

Скрипт для авторизации в админ. панели Битрикса при утере пароля администратора.

Создаем файл `auth.php` в корне сайта и запускаем его из браузера.

```php
<?php
require($_SERVER["DOCUMENT_ROOT"] . "/bitrix/header.php");
global $USER; 
$USER->Authorize(1); 
@unlink(FILE); 
LocalRedirect("/bitrix/admin/"); 
require($_SERVER["DOCUMENT_ROOT"]."/bitrix/footer.php");
```

После запуска скрипта из браузера, файл `auth.php` удаляется с сервера.

<a name="sources"></a>
## Источники

- [Авторизация в админке без пароля (dev.1c-bitrix.ru)](https://dev.1c-bitrix.ru/community/webdev/user/137665/blog/10311/)