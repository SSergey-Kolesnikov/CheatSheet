[&larr;](readme.md "Ubuntu") Подготовка сервера на Ubuntu 16 c Vesta Control Panel под установку 1С-Битрикс
-----------------------------------------------------------------------------------------------------------

## <a name="content"></a> Содержание:

- [Требования к серверу](#server-requirements)
- [Версия и расширения PHP](#php-version-and-extensions)
- [Файл `php.ini`](#file-php-ini)
- [Настройка Vesta Control Panel](#setting-up-vesta-control-panel)
- [Смена версии PHP для сайта](#php-version-change-for-the-site)

## <a name="server-requirements"></a> Требования к серверу [&uarr;](#content "Содержание")

- PHP 7.1 и выше (рекомендуемая версия PHP 7.2)
- Apache 1.3 и выше
- MySQL 5.6 и выше

## <a name="php-version-and-extensions"></a> Версия и расширения PHP [&uarr;](#content "Содержание")

Панель Vesta Control Panel (на момент публикации 0.9.8-26) поставляется с версией PHP 7.0.33 и версия PHP не подходит для установки 1С-Битрикс.

Для установки требуемой версии PHP можно воспользоваться инструкцией "[Несколько версий PHP на Ubuntu 16 c Vesta Control Panel](multiple-php-versions-on-ubuntu-16-with-vesta-control-panel.md)".

> Предполагаем, что установили версию PHP 7.4.

## <a name="file-php-ini"></a> Файл `php.ini` [&uarr;](#content "Содержание")

Для того, чтобы установить 1С-Битрикс, необходимо изменить как минимум два параметра mbstring - это `mbstring.func_overload` и `mbstring.internal_encoding`. По умолчанию эти параметры имеют значения `0` и `no value` соответственно и при таких значениях установщик 1С-Битрикса не даст развернуть CMS.

Версия PHP, которую установили пунктом ранее, будет работать в режиме `CGI/FastCGI` и изменить параметры mbstring в настройках виртуальных хостов не представляется возможным.

Для выхода из ситуации, создаем копию файла `php.ini`:

```markdown
sudo cp /etc/php/7.4/cgi/php.ini /etc/php/7.4/cgi/php-bitrix.ini
```

Теперь у нас есть отдельный файл `/etc/php/7.4/cgi/php-bitrix.ini` и его можно использовать под настройку 1С-Битрикса. Редактируем его и указываем необходимые параметры:

```markdown
date.timezone = "Europe/Moscow"
display_errors = On
mbstring.func_overload = 2
mbstring.internal_encoding = UTF-8
opcache.revalidate_freq = 0
short_open_tag = On
max_input_vars = 10000
post_max_size = 20M
upload_max_filesize = 20M
```

Перезапускаем Apache:

```markdown
sudo service apache2 restart
```

## <a name="setting-up-vesta-control-panel"></a> Настройка Vesta Control Panel [&uarr;](#content "Содержание")

По умолчанию в Vesta Control Panel есть шаблон phpcgi. Копируем файлы этого шаблона:

```markdown
sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.sh /usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.sh
```

```markdown
sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.stpl /usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.stpl
```

```markdown
sudo cp /usr/local/vesta/data/templates/web/apache2/phpcgi.tpl /usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.tpl
```

В файле `/usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.sh` меняем строку

```markdown
wrapper_script='#!/usr/bin/php-cgi -cphp5-cgi.ini'
```

на

```markdown
wrapper_script='#!/usr/bin/php-cgi74 -c/etc/php/7.4/cgi/php-bitrix.ini'
```

Для файла `/usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.sh` права доступа должны быть 755. В случае отличия, меняем права доступа для файла на 755:

```markdown
sudo chmod 755 /usr/local/vesta/data/templates/web/apache2/php7.4-bitrix.sh
```

Перезапускаем Vesta Control Panel:

```markdown
sudo service vesta restart
```

## <a name="php-version-change-for-the-site"></a> Смена версии PHP для сайта [&uarr;](#content "Содержание")

Активация версии PHP 7.4 для 1С-Битрикс выполняется следующим образом:

- Проходим авторизацию в панели управления Vesta Control Panel под логином admin (изменение шаблонов возможно только из под основного аккаунта);
- В случае необходимости на закладке USER авторизуемся под нужным пользователем;
- В категории WEB выбираем нужный домен и нажимаем на кнопку «Редактировать»;
- Находим пункт «Шаблон Web Apache2» и выбираем из выпадающего списка шаблон php7.4-bitrix;
- Нажимаем кнопку «Сохранить».