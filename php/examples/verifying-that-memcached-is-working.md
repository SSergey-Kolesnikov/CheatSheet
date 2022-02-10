[&larr;](readme.md "Примеры") Проверка работы Memcached
-------------------------------------------------------

Создаем PHP-скрипт и указываем данные сервера Memcached.

```php
<?php

$m = new Memcached();
$m->addServer('localhost', 11211);
$m->set('testKey', 'testValue');
print_r($m->getResultMessage());
print_r('<hr />');
var_dump($m->get('testKey'));
```

Запускаем PHP-скрипт из браузера и при успешном выполнении увидим SUCCESS.

```markdown
SUCCESS
string(9) "testValue"
```

А при ошибке увидим FAILED.

```markdown
SERVER HAS FAILED AND IS DISABLED UNTIL TIMED RETRY
bool(false)
```

<a name="sources"></a>
## Источники

- [Как проверить корректно ли работает memcached? (nagg.ru)](https://nagg.ru/2016/03/kak-proverit-korrektno-li-rabotaet-memcached/)