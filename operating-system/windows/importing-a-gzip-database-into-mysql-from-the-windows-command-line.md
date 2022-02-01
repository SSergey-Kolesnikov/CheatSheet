[&larr;](readme.md "Windows") Импорт заархивированной через Gzip БД в MySQL из командной строки Windows
-------------------------------------------------------------------------------------------------------

Скачиваем бинарный файл с сайта [gnuwin32.sourceforge.net](http://gnuwin32.sourceforge.net/packages/gzip.htm) и распаковываем содержимое архива, к примеру в `C:\GnuWin32\Gzip`.

Теперь можно импортировать дамп базы данных со сжатием gz через командную строку Windows.

```markdown
C:\GnuWin32\Gzip\bin\gzip.exe -dc < "<FILE_NAME>.sql.gz" | mysql -u<USER> -p<PASSWORD> <DATABASE>
```

где:

- `C:\GnuWin32\Gzip\bin\gzip.exe` - путь до исполняемого файла;
- `<USER>` - имя пользователя БД;
- `<PASSWORD>` - пароль пользователя БД;
- `<DATABASE>` - имя базы данных;
- `<FILE_NAME>` - имя файла;

<a name="sources"></a>
## Источники

- [Using mysqldump on windows (stackoverflow.com)](https://stackoverflow.com/questions/27409138/using-mysqldump-on-windows)