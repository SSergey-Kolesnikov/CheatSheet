[&larr;](readme.md "Ubuntu") Несколько версий PHP на Ubuntu 16 c Vesta Control Panel
------------------------------------------------------------------------------------

Инструкция по установке дополнительной версии PHP (для примера взята PHP 7.4) на сервере с установленной панелью Vesta Control Panel.

> Предполагается, что установка PHP 7.4 проходит на чистый сервер с операционной системой Ubuntu 16 и установленной панелью Vesta Control Panel.  

## <a name="content"></a> Содержание:
- [Установка PHP 7.4](#install-php-7-4)
- [Настройка Apache](#configure-apache)
- [Шаблоны Vesta Control Panel](#vesta-control-panel-templates)
- [Смена версии PHP для сайта](#php-version-change-for-the-site)
- [Источники](#sources)

## <a name="install-php-7-4"></a> Установка PHP 7.4 [&uarr;](#content)

Обновляем список пакетов:

```markdown
apt-get update
```

Обновляем пакеты:

```markdown
apt-get upgrade
```

Добавляем пакет software-properties-common:

```markdown
apt-get install software-properties-common
```

Добавляем репозиторий PHP из Ondrej:

```markdown
add-apt-repository ppa:ondrej/php
```

Обновляем список пакетов:

```markdown
apt-get update
```

Устанавливаем PHP 7.4:

```markdown
apt-get install php7.4
```

Устанавливаем расширения для PHP 7.4:

```markdown
apt-get install php7.4-cgi php7.4-cli php7.4-common php7.4-curl php7.4-gd php7.4-imap php7.4-intl php7.4-json php7.4-ldap php7.4-mbstring php7.4-mysql php7.4-opcache php7.4-pspell php7.4-readline php7.4-soap php7.4-xml
```

Создаем символическую ссылку для новой установленной PHP версии:

```markdown
ln -sf /usr/bin/php-cgi7.4 /usr/bin/php-cgi74
```

## <a name="configure-apache"></a> Настройка Apache [&uarr;](#content)

Активируем CGI модуль веб-сервера:

```markdown
a2enmod actions cgi
```

Перезапускаем Apache:

```markdown
service apache2 restart
```

## <a name="vesta-control-panel-templates"></a> Шаблоны Vesta Control Panel [&uarr;](#content)

По умолчанию в Vesta Control Panel есть шаблон phpcgi. Копируем файлы этого шаблона:

```markdown
cp /usr/local/vesta/data/templates/web/apache2/phpcgi.sh /usr/local/vesta/data/templates/web/apache2/php7.4.sh
```

```markdown
cp /usr/local/vesta/data/templates/web/apache2/phpcgi.stpl /usr/local/vesta/data/templates/web/apache2/php7.4.stpl
```

```markdown
cp /usr/local/vesta/data/templates/web/apache2/phpcgi.tpl /usr/local/vesta/data/templates/web/apache2/php7.4.tpl
```

В только что скопированном файле `/usr/local/vesta/data/templates/web/apache2/php7.4.sh` меняем строку

```markdown
wrapper_script='#!/usr/bin/php-cgi -cphp5-cgi.ini'
```

на

```markdown
wrapper_script='#!/usr/bin/php-cgi74 -c/etc/php/7.4/cgi/php.ini'
```

Для файла `/usr/local/vesta/data/templates/web/apache2/php7.4.sh` права доступа должны быть 755. В случае отличия, меняем права доступа для файла на на 755:

```markdown
chmod 755 /usr/local/vesta/data/templates/web/apache2/php7.4.sh
```

Перезапускаем Vesta Control Panel:

```markdown
service vesta restart
```

## <a name="php-version-change-for-the-site"></a> Смена версии PHP для сайта [&uarr;](#content)

Активация версии PHP 7.4 выполняется следующим образом:

- Проходим авторизацию в панели управления Vesta Control Panel под логином admin (изменение шаблонов возможно только из под основного аккаунта);
- В случае необходимости на закладке USER авторизуемся под нужным пользователем;
- В категории WEB выбираем нужный домен и нажимаем на кнопку «Редактировать»;
- Находим пункт «Шаблон Web Apache2» и выбираем из выпадающего списка шаблон php7.4;
- Нажимаем кнопку «Сохранить».


## <a name="sources"></a> Источники [&uarr;](#content)

- [How to install PHP (7.2, 7.3 or 7.4) on Ubuntu (thishosting.rocks)](https://thishosting.rocks/install-php-on-ubuntu/)
- [Как установить PHP 7.2 на Ubuntu 16.04 (andreyex.ru)](https://andreyex.ru/ubuntu/kak-ustanovit-php-7-2-na-ubuntu-16-04/)
- [Использование нескольких версий PHP в панели VestaCP (netpoint-dc.com)](https://netpoint-dc.com/blog/multiversionnost-php-dlja-raboty-s-panelju-upravlenija-vestacp/)
- [Мультиверсионность php на сервере с VestaCP (anikin.pw)](https://anikin.pw/all/multiversionnost-php-na-servere-s-vestacp/)