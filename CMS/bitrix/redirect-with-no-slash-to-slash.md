[&larr;](readme.md "Битрикс") Редирект с без слеша на слеш
----------------------------------------------------------

В файл `.htaccess` в условие `mod_rewrite` добавить правило:

```markdown
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-l
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_URI} ^(.*/[^/\.]+)$
RewriteRule ^(.*)$ http://%{HTTP_HOST}/$1/ [R=301,L]
```

В итоге должно получиться, к примеру:

```markdown
<IfModule mod_rewrite.c>
    Options +FollowSymLinks
    RewriteEngine On

    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-l
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_URI} ^(.*/[^/\.]+)$
    RewriteRule ^(.*)$ http://%{HTTP_HOST}/$1/ [R=301,L]

    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-l
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !/bitrix/urlrewrite.php$
    RewriteRule ^(.*)$ /bitrix/urlrewrite.php [L]
    RewriteRule .* - [E=REMOTE_USER:%{HTTP:Authorization}]
</IfModule>
```

### Источник

- [Ссылка со слешем в конце и без — разные страницы. Почему?) (dev.1c-bitrix.ru)](https://dev.1c-bitrix.ru/support/forum/messages/forum6/topic36842/message202369/#message202369)