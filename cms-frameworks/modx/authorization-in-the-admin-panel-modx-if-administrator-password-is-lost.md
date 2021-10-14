[&larr;](readme.md "MODX") Авторизация в админ. панели MODX, если потерян пароль администратора
-----------------------------------------------------------------------------------------------

Скрипт для авторизации в админ. панели MODX при утере пароля администратора.

Создаем файл `auth.php` в корне сайта и запускаем его из браузера.

```php
<?
define('MODX_API_MODE', true);
require 'index.php';

$member = $modx->getObject('modUserGroupMember', array('user_group' => 1));
$user = $modx->getObject('modUser', $member->member);
$user->addSessionContext('mgr');
unlink(basename(__FILE__));

$modx->sendRedirect('/manager/');
```

После запуска скрипта из браузера, файл `auth.php` удаляется с сервера.

## Источник

- [Авторизация в админке сайта MODX (если потеряли пароль админа) (ilyaut.ru)](https://ilyaut.ru/cheats/authorization-in-the-admin-area-of-modx-if-lost-admin-password/)