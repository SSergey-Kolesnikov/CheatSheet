[&larr;](readme.md "Windows") Настройка связки OpenServer + Xdebug + PhpStorm
-----------------------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Файл `php.ini`](#file-php-ini)
- [Настройка PhpStorm](#setting-up-phpstorm)
- [Плагин для браузера](#browser-plugin)
- [Источники](#sources)

<a name="file-php-ini"></a>
## Файл `php.ini`

Минимальный набор настроек для Xdebug:

```markdown
zend_extension = xdebug

xdebug.mode = debug
xdebug.client_host = "localhost"
xdebug.client_port = 9003
xdebug.idekey = "PHPSTORM"
```

> После изменений в файле `php.ini` не забываем перезапустить Apache.

<a name="setting-up-phpstorm"></a>
## Настройка PhpStorm

Открываем настройки `File` -> `Settings`, переходим в настройки PHP `Languages & Frameworks` -> `PHP` и нажимаем на "троеточие" напротив `CLI Interpreter`. В открывшемся окне нажимаем на "плюсик", в поле `Name` указываем версию PHP (к примеру `PHP 7.4`), в блоке `General` и поле `PHP executable` указываем путь до PHP интерпретатора. Как только путь до интерпретатора указан, показывается версия PHP в поле `PHP version` и используемый дебагер в поле `Debugger`. Сохраняем настройки.

Открываем настройки `File` -> `Settings`, переходим в `Languages & Frameworks` -> `PHP` -> `Debug`. В блоке `Xdebug` указываем порт `9003` (ранее указывался в `php.ini`) в поле `Debug port`, чекбоксы `Can accept external connections` и `Resolve breakpoint if it's not available on the current line (Xdebug 2.8+)` оставляем отмеченными, а с чекбоксов `Force break at first line when to path mapping specifield` и `Force break at first line when a script is outside the project` снимаем выделение.

Открываем настройки `File` -> `Settings`, переходим в `Languages & Frameworks` -> `PHP` -> `Servers`. Нажимаем на "плюсик", указываем в поле `Name` наименование сервера (указываю домен), в поле `Host` домен, поле `Port` оставляем по умолчанию, в поле `Debugger` должен быть указан `Xdebug`. Сохраняем настройки.

В правом верхнем углу приложения на панели дебага кликаем по выпадающему списку и выбираем `Edit Configuration`. В открывшемся окне `Run/Debug Configurations` кликаем "плюсик" и выбираем `PHP Remote Debug`, указываем наименование в поле `Name` (к примеру `XDebug`), в блоке `Configuration` отмечаем чекбокс `Filter debug onnection by IDE key`, в выпадающем списке `Server` выбираем ранее созданный сервер и в поле `IDE key (session id)` указываем ключ `PHPSTORM` (ранее указывался в `php.ini`). Сохраняем настройки.

<a name="browser-plugin"></a>
## Плагин для браузера

Для браузера Chrome устанавливаем плагин [Xdebug helper](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc) и в его настройках в блоке `IDE key` в выпадающем списке выбираем `PhpStorm`.

<a name="sources"></a>
## Источники

- [Отладка PHP 8 с помощью Xdebug 3 в PHPStorm (php.zone)](https://php.zone/kurs-php-dlya-nachinayushih/otladka-php-koda-s-pomoshchyu-xdebug-v-phpstorm)
- [Отладка PHP 7 с помощью Xdebug в PHPStorm (php.zone)](https://php.zone/post/otladka-php-7-s-pomoshchyu-xdebug-v-phpstorm)
- [Установка и настройка Xdebug + PHPStorm в Ubuntu 16.04 / Elementary OS 0.4 (Loki) / Mint 18 (freshnotes.top)](https://freshnotes.top/2016/12/ustanovka-i-nastrojka-xdebug-phpstorm-v-ubuntu-16-04-elementary-os-0-4-loki-mint-18/)