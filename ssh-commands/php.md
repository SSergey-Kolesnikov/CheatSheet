[&larr;](readme.md "SSH команды") PHP
-------------------------------------

#### Версия PHP

```markdown
php -v
```

#### Путь, куда установлен PHP

```markdown
which php
```

#### Список доступных расширений PHP

```markdown
php -m
```

#### Список доступных расширений PHP

```markdown
apt-cache search php|egrep ^php<VERSION>
```

где:

- `<VERSION>` - номер версии PHP

Результатом команды `apt-cache search php|egrep ^php` будет:

```markdown
php-common - Common files for PHP packages
php7.0 - server-side, HTML-embedded scripting language (metapackage)
php7.0-cgi - server-side, HTML-embedded scripting language (CGI binary)
php7.0-cli - command-line interpreter for the PHP scripting language
php7.0-common - documentation, examples and common module for PHP
...
php7.4-tidy - tidy module for PHP
php7.4-xml - DOM, SimpleXML, XML, and XSL module for PHP
php7.4-xmlrpc - XMLRPC-EPI module for PHP
php7.4-xsl - XSL module for PHP (dummy)
php7.4-zip - Zip module for PHP
```

Результатом команды `apt-cache search php|egrep ^php7.4` будет:

```markdown
php7.4 - server-side, HTML-embedded scripting language (metapackage)
php7.4-bcmath - Bcmath module for PHP
php7.4-bz2 - bzip2 module for PHP
php7.4-cgi - server-side, HTML-embedded scripting language (CGI binary)
php7.4-cli - command-line interpreter for the PHP scripting language
...
php7.4-tidy - tidy module for PHP
php7.4-xml - DOM, SimpleXML, XML, and XSL module for PHP
php7.4-xmlrpc - XMLRPC-EPI module for PHP
php7.4-xsl - XSL module for PHP (dummy)
php7.4-zip - Zip module for PHP
```

#### Список установленных расширений для PHP

```markdown
dpkg --list | grep php<VERSION>
```

где:

- `<VERSION>` - номер версии PHP

Результатом команды `dpkg --list | grep php` будет вывод всех установленных расшинений для PHP:

```markdown
ii  libapache2-mod-php                    1:7.0+35ubuntu6.1                               all          server-side, HTML-embedded scripting language (Apache 2 module) (default)
ii  libapache2-mod-php7.0                 7.0.33-29+ubuntu16.04.1+deb.sury.org+1          amd64        server-side, HTML-embedded scripting language (Apache 2 module)
ii  libapache2-mod-php7.4                 7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        server-side, HTML-embedded scripting language (Apache 2 module)
ii  php-auth                              1.6.4-1build1                                   all          Creating an authentication system
...
ii  php7.4-soap                           7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        SOAP module for PHP
ii  php7.4-xml                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        DOM, SimpleXML, XML, and XSL module for PHP
ii  php7.4-zip                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        Zip module for PHP
ii  phpmyadmin                            4:4.5.4.1-2ubuntu2.1                            all          MySQL web administration tool
ii  vesta-php                             0.9.8-26                                        amd64        Vesta php-fpm
```

Результатом команды `dpkg --list | grep php7.4` будет вывод всех установленных расшинений для PHP 7.4:

```markdown
ii  libapache2-mod-php7.4                 7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        server-side, HTML-embedded scripting language (Apache 2 module)
ii  php7.4                                7.4.7-1+ubuntu16.04.1+deb.sury.org+1            all          server-side, HTML-embedded scripting language (metapackage)
ii  php7.4-cgi                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        server-side, HTML-embedded scripting language (CGI binary)
ii  php7.4-cli                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        command-line interpreter for the PHP scripting language
ii  php7.4-common                         7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        documentation, examples and common module for PHP
...
ii  php7.4-pspell                         7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        pspell module for PHP
ii  php7.4-readline                       7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        readline module for PHP
ii  php7.4-soap                           7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        SOAP module for PHP
ii  php7.4-xml                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        DOM, SimpleXML, XML, and XSL module for PHP
ii  php7.4-zip                            7.4.7-1+ubuntu16.04.1+deb.sury.org+1            amd64        Zip module for PHP
```

#### Поиск пакета PHP по именам пакетов

```markdown
apt search php<VERSION>
```

где:

- `<VERSION>` - номер версии PHP

Результатом команды `apt search php` будет вывод всех пакетов для PHP:

```markdown
Sorting... Done
Full Text Search... Done
php-markdown/xenial,xenial 1.6.0-1build1 all
  PHP library for rendering Markdown data

php-mbstring/xenial,xenial 2:7.4+76+ubuntu16.04.1+deb.sury.org+9 all [upgradable from: 1:7.0+35ubuntu6.1]
  MBSTRING module for PHP [default]

php-mcrypt/xenial-updates,xenial-updates,now 1:7.0+35ubuntu6.1 all [installed,automatic]
  libmcrypt module for PHP [default]

php-mdb2/xenial,xenial,now 2.5.0b5-1build1 all [installed,automatic]
  merge of the PEAR DB and Metabase php database abstraction layers

php-mdb2-driver-mysql/xenial,xenial 1.5.0b4-1ubuntu1 all
  PHP PEAR module to provide a MySQL driver for MDB2

...

php7.4-tidy/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  tidy module for PHP

php7.4-xml/xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64 [installed]
  DOM, SimpleXML, XML, and XSL module for PHP

php7.4-xmlrpc/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  XMLRPC-EPI module for PHP

php7.4-xsl/xenial,xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 all
  XSL module for PHP (dummy)

php7.4-zip/xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64 [installed]
  Zip module for PHP

```

Результатом команды `apt search php7.4` будет вывод всех пакетов для PHP 7.4:

```markdown
Sorting... Done
Full Text Search... Done
libapache2-mod-php7.4/xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64 [installed,automatic]
  server-side, HTML-embedded scripting language (Apache 2 module)

libphp7.4-embed/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  HTML-embedded scripting language (Embedded SAPI library)

php7.4/xenial,xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 all [installed]
  server-side, HTML-embedded scripting language (metapackage)

php7.4-bcmath/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  Bcmath module for PHP

php7.4-bz2/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  bzip2 module for PHP

...

php7.4-tidy/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  tidy module for PHP

php7.4-xml/xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64 [installed]
  DOM, SimpleXML, XML, and XSL module for PHP

php7.4-xmlrpc/xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64
  XMLRPC-EPI module for PHP

php7.4-xsl/xenial,xenial 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 all
  XSL module for PHP (dummy)

php7.4-zip/xenial,now 7.4.7-1+ubuntu16.04.1+deb.sury.org+1 amd64 [installed]
  Zip module for PHP

```

## Источник

- [Как посмотреть список установленных расширений php на сервере с консоли (mb4.ru)](https://mb4.ru/programming/php/1162-ssh-list-extension-loaded.html)