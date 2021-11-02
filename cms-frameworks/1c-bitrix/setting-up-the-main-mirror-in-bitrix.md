[&larr;](readme.md "1С-Битрикс") Настройка главного зеркала в Битриксе
----------------------------------------------------------------------

## <a name="content"></a> Содержание:

- [Редирект на https и www](#redirect-to-https-and-www)
- [Источник](#source)

## Редирект на https и www

### Вариант 1

В файл `.htaccess` в условие `mod_rewrite` добавляем правило:

```markdown
RewriteCond %{HTTP_HOST} ^<YOUR_SITE>\.ru$ [NC]
RewriteRule ^(.*)$ https://www.<YOUR_SITE>.ru/$1 [R=301,L]

RewriteCond %{ENV:HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

где:

- `<YOUR_SITE>` - домен вашего сайта;

В итоге должно получиться, к примеру:

```markdown
<IfModule mod_rewrite.c>
    Options +FollowSymLinks
    RewriteEngine On
    
    RewriteCond %{HTTP_HOST} ^<YOUR_SITE>\.ru$ [NC]
    RewriteRule ^(.*)$ https://www.<YOUR_SITE>.ru/$1 [R=301,L]
    
    RewriteCond %{ENV:HTTPS} !on
    RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
    
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-l
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !/bitrix/urlrewrite.php$
    RewriteRule ^(.*)$ /bitrix/urlrewrite.php [L]
    RewriteRule .* - [E=REMOTE_USER:%{HTTP:Authorization}]
</IfModule>
```

где:

- `<YOUR_SITE>` - домен вашего сайта;

### Вариант 2

В файл `.htaccess` в условие `mod_rewrite` добавляем правило:

```markdown
RewriteCond %{HTTP_HOST} !^www\.(.*) [NC]
RewriteRule ^(.*)$ https://www.%{SERVER_NAME}%{REQUEST_URI} [R=301,L]

RewriteCond %{SERVER_PORT} !^443$ 
RewriteRule ^(.*)$ https://%{SERVER_NAME}%{REQUEST_URI} [R=301,L]
```

В итоге должно получиться, к примеру:

```markdown
<IfModule mod_rewrite.c>
    Options +FollowSymLinks
    RewriteEngine On
    
    RewriteCond %{HTTP_HOST} !^www\.(.*) [NC]
    RewriteRule ^(.*)$ https://www.%{SERVER_NAME}%{REQUEST_URI} [R=301,L]
    
    RewriteCond %{SERVER_PORT} !^443$ 
    RewriteRule ^(.*)$ https://%{SERVER_NAME}%{REQUEST_URI} [R=301,L]
    
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-l
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !/bitrix/urlrewrite.php$
    RewriteRule ^(.*)$ /bitrix/urlrewrite.php [L]
    RewriteRule .* - [E=REMOTE_USER:%{HTTP:Authorization}]
</IfModule>
```

## <a name="source"></a> Источник

- [Правильный редирект в битрикс (el-komp.ru)](https://www.el-komp.ru/pravilnyj-redirekt-v-bitriks.html)