[&larr;](readme.md "Ubuntu") Установка Laravel на Ubuntu 16 c Vesta Control Panel
---------------------------------------------------------------------------------

Инструкция по установке последней версии Laravel (на момент публикации 7.19.0) на сервере с операционной системой Ubuntu 16 и установленной панелью Vesta Control Panel.

## <a name="content"></a> Содержание:

- [Требования к серверу](#server-requirements)
- [Версия и расширения PHP](#php-version-and-extensions)
- [Настройка Vesta Control Panel](#setting-up-vesta-control-panel)
- [Смена версии PHP для сайта](#php-version-change-for-the-site)
- [Composer](#composer)
- [Установка Laravel](#install-laravel)
- [Источники](#sources)

## <a name="server-requirements"></a> Требования к серверу [&uarr;](#content "Содержание")

Фреймворк Laravel предъявляет системные требования к серверу и он должен соответствовать им.

Конечно же, виртуальная машина [Laravel Homestead](https://laravel.com/docs/7.x/homestead) соответствует всем этим требованиям, поэтому рекомендуется использовать Homestead в качестве основной локальной среды разработки с Laravel. Однако, если не используется Homestead, то необходимо убедиться, что сервер соответствует им:

- PHP >= 7.2.5
- BCMath PHP Extension
- Ctype PHP Extension
- Fileinfo PHP extension
- JSON PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

## <a name="php-version-and-extensions"></a> Версия и расширения PHP [&uarr;](#content "Содержание")

Панель Vesta Control Panel (на момент публикации 0.9.8-26) поставляется с версией PHP 7.0.33 и версия PHP не подходит для установки последней версии Laravel.

Для установки требуемой версии PHP можно воспользоваться инструкцией "[Несколько версий PHP на Ubuntu 16 c Vesta Control Panel](multiple-php-versions-on-ubuntu-16-with-vesta-control-panel.md)".

> Предполагаем, что установили версию PHP 7.4.

## <a name="setting-up-vesta-control-panel"></a> Настройка Vesta Control Panel [&uarr;](#content "Содержание")

По умолчанию в Vesta Control Panel есть шаблон phpcgi. Копируем файлы этого шаблона:

```markdown
user@computer:~$ sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.sh /usr/local/vesta/data/templates/web/apache2/php7.4-laravel.sh
```

```markdown
user@computer:~$ sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.stpl /usr/local/vesta/data/templates/web/apache2/php7.4-laravel.stpl
```

```markdown
user@computer:~$ sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.tpl /usr/local/vesta/data/templates/web/apache2/php7.4-laravel.tpl
```

В файле `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.sh` меняем строку

```markdown
wrapper_script='#!/usr/bin/php-cgi -cphp5-cgi.ini'
```

на

```markdown
wrapper_script='#!/usr/bin/php-cgi74 -c/etc/php/7.4/cgi/php.ini'
```

Для файла `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.sh` права доступа должны быть 755. В случае отличия, меняем права доступа для файла на 755:

```markdown
user@computer:~$ sudo chmod 755 /usr/local/vesta/data/templates/web/apache2/php7.4-laravel.sh
```

В файле `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.stpl` меняем строку

```markdown
DocumentRoot %sdocroot%
```

на

```markdown
DocumentRoot %sdocroot%/public
```

> Файл шаблона `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.stpl`:
> 
> ```markdown
> <VirtualHost %ip%:%web_ssl_port%>
> 
>     ServerName %domain_idn%
>     %alias_string%
>     ServerAdmin %email%
>     DocumentRoot %sdocroot%/public
>     ScriptAlias /cgi-bin/ %home%/%user%/web/%domain%/cgi-bin/
>     Alias /vstats/ %home%/%user%/web/%domain%/stats/
>     Alias /error/ %home%/%user%/web/%domain%/document_errors/
>     SuexecUserGroup %user% %group%
>     CustomLog /var/log/%web_system%/domains/%domain%.bytes bytes
>     CustomLog /var/log/%web_system%/domains/%domain%.log combined
>     ErrorLog /var/log/%web_system%/domains/%domain%.error.log
>     <Directory %sdocroot%>
>         SSLRequireSSL
>         AllowOverride All
>         Options +Includes -Indexes +ExecCGI
>         php_admin_value open_basedir %docroot%:%home%/%user%/tmp
>         php_admin_value upload_tmp_dir %home%/%user%/tmp
>         php_admin_value session.save_path %home%/%user%/tmp
>         Action phpcgi-script /cgi-bin/php
>         <Files *.php>
>             SetHandler phpcgi-script
>         </Files>
>     </Directory>
>     <Directory %home%/%user%/web/%domain%/stats>
>         AllowOverride All
>     </Directory>
>     SSLEngine on
>     SSLVerifyClient none
>     SSLCertificateFile %ssl_crt%
>     SSLCertificateKeyFile %ssl_key%
>     %ssl_ca_str%SSLCertificateChainFile %ssl_ca%
> 
>     IncludeOptional %home%/%user%/conf/web/s%web_system%.%domain%.conf*
> 
> </VirtualHost>
> 
> 
> ```

В файле `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.tpl` меняем строку

```markdown
DocumentRoot %docroot%
```

на

```markdown
DocumentRoot %docroot%/public
```

> Файл шаблона `/usr/local/vesta/data/templates/web/apache2/php7.4-laravel.tpl`:
> 
> ```markdown
> <VirtualHost %ip%:%web_port%>
> 
>     ServerName %domain_idn%
>     %alias_string%
>     ServerAdmin %email%
>     DocumentRoot %docroot%/public
>     ScriptAlias /cgi-bin/ %home%/%user%/web/%domain%/cgi-bin/
>     Alias /vstats/ %home%/%user%/web/%domain%/stats/
>     Alias /error/ %home%/%user%/web/%domain%/document_errors/
>     SuexecUserGroup %user% %group%
>     CustomLog /var/log/%web_system%/domains/%domain%.bytes bytes
>     CustomLog /var/log/%web_system%/domains/%domain%.log combined
>     ErrorLog /var/log/%web_system%/domains/%domain%.error.log
>     <Directory %docroot%>
>         AllowOverride All
>         Options +Includes -Indexes +ExecCGI
>         php_admin_value open_basedir %docroot%:%home%/%user%/tmp
>         php_admin_value upload_tmp_dir %home%/%user%/tmp
>         php_admin_value session.save_path %home%/%user%/tmp
>         Action phpcgi-script /cgi-bin/php
>         <Files *.php>
>             SetHandler phpcgi-script
>         </Files>
>     </Directory>
>     <Directory %home%/%user%/web/%domain%/stats>
>         AllowOverride All
>     </Directory>
>     IncludeOptional %home%/%user%/conf/web/%web_system%.%domain%.conf*
> 
> </VirtualHost>
> 
> 
> ```

Перезапускаем Vesta Control Panel:

```markdown
user@computer:~$ sudo service vesta restart
```

## <a name="php-version-change-for-the-site"></a> Смена версии PHP для сайта [&uarr;](#content "Содержание")

Активация версии PHP 7.4 для Laravel выполняется следующим образом:

- Проходим авторизацию в панели управления Vesta Control Panel под логином admin (изменение шаблонов возможно только из под основного аккаунта);
- В случае необходимости на закладке USER авторизуемся под нужным пользователем;
- В категории WEB выбираем нужный домен и нажимаем на кнопку «Редактировать»;
- Находим пункт «Шаблон Web Apache2» и выбираем из выпадающего списка шаблон php7.4-laravel;
- Нажимаем кнопку «Сохранить».

## <a name="composer"></a> Composer [&uarr;](#content "Содержание")

Laravel использует [Composer](https://getcomposer.org/) для управления зависимостями. Поэтому сначала устанавливаем Composer, а затем Laravel.

Для установки Composer можно воспользоваться инструкцией "[Установка Composer на Ubuntu 16](install-composer-on-ubuntu-16.md)".

## <a name="install-laravel"></a> Установка Laravel [&uarr;](#content "Содержание")

Переходим в домашнюю папку:

```markdown
user@computer:~$ cd ~
```

Скачиваем установщик Laravel:

```markdown
user@computer:~$ composer global require laravel/installer
```

Далее обязательно помещаем общесистемный каталог bin от Composer в свой каталог $PATH. Это позволит Ubuntu распознать исполняемый файл Laravel.

```markdown
user@computer:~$ echo 'export PATH="$PATH:$HOME/.config/composer/vendor/bin"' >> ~/.bashrc
```

Перезагружаем пути:

```markdown
user@computer:~$ source ~/.bashrc
```

Переходим в папку с проектом:

```markdown
user@computer:~$ cd /home/<USER>/web/<DOMAIN>/public_html
```

где:

- `<USER>` - пользователь в Vesta Control Panel
- `<DOMAIN>` - домен

Устанавливаем Laravel:

```markdown
user@computer:~$ laravel new
```

или

```markdown
user@computer:~$ composer create-project --prefer-dist laravel/laravel .
```

> Laravel устанавливается в текущую папку.

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [Installation - Laravel (laravel.com)](https://laravel.com/docs/7.x)
- [Установка | Laravel по-русски (laravel.ru)](https://laravel.ru/docs/v5/installation)
- [Установка (Laravel 5.4) — Laravel Framework Russian Community (laravel.su)](https://laravel.su/docs/5.4/installation)
- [Как установить Laravel в корневую директорию? (qna.habr.com)](https://qna.habr.com/q/542836)
- [Laravel on VestaCP (gist.github.com)](https://gist.github.com/peterbrinck/26684a078027a0c0c978a470be27edc3)
- [need LARAVEL templates nginx and httpd ? (forum.vestacp.com)](https://forum.vestacp.com/viewtopic.php?t=6460)
- [vesta_templates (github.com)](https://github.com/errogaht/vesta_templates)