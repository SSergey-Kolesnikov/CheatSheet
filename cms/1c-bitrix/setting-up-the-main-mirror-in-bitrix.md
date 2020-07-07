[&larr;](readme.md "1С-Битрикс") Настройка главного зеркала в Битриксе
----------------------------------------------------------------------

## <a name="content"></a> Содержание:

- [Редирект на https и www](#redirect-to-https-and-www)
- [Источник](#source)

## Редирект на https и www [&uarr;](#content "Содержание")

В файл `.htaccess` в условие `mod_rewrite` добавляем правило:

```markdown
RewriteCond %{HTTP_HOST} ^YOUR_SITE\.ru$ [NC]
RewriteRule ^(.*)$ https://www.YOUR_SITE.ru/$1 [R=301,L]

RewriteCond %{ENV:HTTPS} !on
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

В итоге должно получиться, к примеру:

```markdown
<IfModule mod_rewrite.c>
    Options +FollowSymLinks
    RewriteEngine On
    
    RewriteCond %{HTTP_HOST} ^YOUR_SITE\.ru$ [NC]
    RewriteRule ^(.*)$ https://www.YOUR_SITE.ru/$1 [R=301,L]
    
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

## <a name="source"></a> Источник [&uarr;](#content "Содержание")

- [Правильный редирект в битрикс (el-komp.ru)](https://www.el-komp.ru/pravilnyj-redirekt-v-bitriks.html)