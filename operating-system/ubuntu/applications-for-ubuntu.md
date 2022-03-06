[&larr;](readme.md "Ubuntu") Приложения для Ubuntu
--------------------------------------------------

<a name="content"></a>
## Содержание:

- [Браузеры](#browsers)
  - [Google Chrome](#google-chrome)
  - [Mozilla Firefox](#mozilla-firefox)
- [Связь](#communications)
  - [Skype](#skype)
  - [Telegram](#telegram)
  - [Zoom](#zoom)
- [Утилиты](#utilities)
  - [CopyQ](#copyq)
  - [Gnome Tweak Tool](#gnome-tweak-tool)
- [Web](#web)
  - [Composer](#composer)
  - [DBeaver](#dbeaver)
  - [Git](#git)
  - [PhpStorm](#phpstorm)
  - [Sublime Text](#sublime-text)
  - [TablePlus](#tableplus)
- [Источники](#sources)

<a name="browsers"></a>
## Браузеры

<a name="google-chrome"></a>
### Google Chrome

Сайт: [google.ru/chrome/](https://www.google.ru/chrome/)   
Скачать: [google.ru/chrome/](https://www.google.ru/chrome/)

<a name="mozilla-firefox"></a>
### Mozilla Firefox

Сайт: [mozilla.org/ru/firefox/](https://www.mozilla.org/ru/firefox/)   
Скачать: [mozilla.org/ru/firefox/](https://www.mozilla.org/ru/firefox/)

<a name="communications"></a>
## Связь

<a name="skype"></a>
### Skype

Сайт: [skype.com/ru/](https://www.skype.com/ru/)  
Скачать: [skype.com/ru/get-skype/](https://www.skype.com/ru/get-skype/)

<a name="telegram"></a>
### Telegram

Сайт: [telegram.org](https://telegram.org/)  
Скачать: [desktop.telegram.org](https://desktop.telegram.org/)

<a name="zoom"></a>
### Zoom

> Проприетарная программа для организации видеоконференций. Она предоставляет сервис видеотелефонии, который позволяет подключать одновременно до 100 устройств бесплатно, с 40-минутным ограничением для бесплатных аккаунтов. Пользователи имеют возможность повысить уровень обслуживания, используя один из тарифных планов, с максимальным числом подключений до 500 человек одновременно, без ограничений по времени.

Сайт: [zoom.us](https://zoom.us/)  
Скачать: [zoom.us/download](https://zoom.us/download#client_4meeting)

<a name="utilities"></a>
## Утилиты

<a name="copyq"></a>
### CopyQ

Сайт: [hluk.github.io/CopyQ/](https://hluk.github.io/CopyQ/)  
Скачать: [github.com/hluk/CopyQ/releases](https://github.com/hluk/CopyQ/releases)

#### Установка

```markdown
user@computer:~$ sudo apt install copyq
```

<a name="gnome-tweak-tool"></a>
### Gnome Tweak Tool

Сайт: [wiki.gnome.org/Apps/Tweaks](https://wiki.gnome.org/Apps/Tweaks)  

#### Установка

```markdown
user@computer:~$ sudo apt install gnome-tweak-tool
```

<a name="composer"></a>
### Composer

>  Пакетный менеджер уровня приложений для языка программирования PHP, который предоставляет средства по управлению зависимостями в PHP-приложении.

Сайт: [getcomposer.org](https://getcomposer.org/)   
Скачать: [getcomposer.org/download/](https://getcomposer.org/download/)  
Лицензия: MIT

#### Установка

Установка Composer на Ubutu описана в "[Установка Composer на Ubuntu 16](install-composer-on-ubuntu-16.md)".

<a name="dbeaver"></a>
### DBeaver

>  Бесплатный многоплатформенный инструмент для работы с базами данных для разработчиков, администраторов баз данных, аналитиков и всех, кому необходимо работать с базами данных. Поддерживает все популярные базы данных: MySQL, PostgreSQL, SQLite, Oracle, DB2, SQL Server, Sybase, MS Access, Teradata, Firebird, Apache Hive, Phoenix, Presto и др.

Сайт: [dbeaver.io](https://dbeaver.io/)   
Скачать: [dbeaver.io/download/](https://dbeaver.io/download/)  
Лицензия: Apache License

#### Установка

Последняя стабильная версия из PPA репозитория

```markdown
user@computer:~$ sudo add-apt-repository ppa:serge-rider/dbeaver-ce
```

```markdown
user@computer:~$ sudo apt-get update
```

```markdown
user@computer:~$ sudo apt-get install dbeaver-ce
```

<a name="git"></a>
### Git

> Распределённая система управления версиями.

Сайт: [git-scm.com](https://git-scm.com/)   
Скачать: [git-scm.com/download/linux](https://git-scm.com/download/linux)  
Лицензия: GNU GPL 2

#### Установка

Последняя стабильная версия из официального репозитория

```markdown
user@computer:~$ sudo apt-get install git
```

Последняя стабильная версия из PPA репозитория

```markdown
user@computer:~$ sudo add-apt-repository ppa:git-core/ppa
```

```markdown
user@computer:~$ sudo apt update; sudo apt install git
```

<a name="phpstorm"></a>
### PhpStorm

> Коммерческая кросс-платформенная интегрированная среда разработки для PHP.
>
> PhpStorm представляет собой интеллектуальный редактор для PHP, HTML и JavaScript с возможностями анализа кода на лету, предотвращения ошибок в коде и автоматизированными средствами рефакторинга для PHP и JavaScript. Автодополнение кода в PhpStorm поддерживает спецификацию PHP 5.3 и выше. Имеется полноценный SQL-редактор с возможностью редактирования полученных результатов запросов.

Сайт: [jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/)   
Скачать: [jetbrains.com/phpstorm/download/](https://www.jetbrains.com/phpstorm/download/#section=linux)  
Лицензия: проприетарная (платная с 30 дневной пробной версией)

#### Установка

```markdown
user@computer:~$ sudo snap install phpstorm --classic
```

<a name="sublime-text"></a>
### Sublime Text

> Проприетарный текстовый редактор.

Сайт: [sublimetext.com](https://www.sublimetext.com/)
Скачать: [sublimetext.com/download](https://www.sublimetext.com/download)  
Лицензия: проприетарная (разработчик позволяет бесплатно и без ограничений ознакомиться с продуктом, однако программа уведомляет о необходимости приобретения лицензии)

<a name="tableplus"></a>
### TablePlus

> Современный инструмент с элегантным пользовательским интерфейсом, который позволяет одновременно управлять несколькими базами данных, такими как MySQL, PostgreSQL, SQLite, Microsoft SQL Server и другими.

Сайт: [tableplus.com](https://tableplus.com/)  
Скачать: [tableplus.com/blog/2019/10/tableplus-linux-installation.html](https://tableplus.com/blog/2019/10/tableplus-linux-installation.html)  
Лицензия: проприетарная (бесплатная пробная версия ограничена 2 открытыми вкладками, 2 открытыми окнами, 2 расширенными фильтрами одновременно)

#### Установка

```markdown
user@computer:~$ wget -qO - http://deb.tableplus.com/apt.tableplus.com.gpg.key | sudo apt-key add -
```

```markdown
user@computer:~$ sudo add-apt-repository "deb [arch=amd64] https://deb.tableplus.com/debian/20 tableplus main"
```

```markdown
user@computer:~$ sudo apt update
```

```markdown
user@computer:~$ sudo apt install tableplus
```

<a name="sources"></a>
## Источники

- [Установка Gnome Tweak Tool в Ubuntu (losst.ru)](https://losst.ru/ustanovka-gnome-tweak-tool-v-ubuntu)