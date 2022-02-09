[&larr;](readme.md "Windows") Консольные команды Windows
--------------------------------------------------------

<a name="content"></a>
## Содержание:

- [Команды](#commands)
    - [Создание каталога](#create-a-directory)
    - [Копирование каталога](#copying-a-directory)
    - [Копирование файла](#file-copy)
    - [Удаление каталога](#deleting-a-directory)
    - [Символическая ссылка на каталог](#symbolic-link-to-directory)
- [Источники](#sources)

<a name="commands"></a>
## Команды

<a name="create-a-directory"></a>
#### Создание каталога

```markdown
C:\> md "<PATH>"
```

где:

- `<PATH>` - путь до нового каталога;

<a name="copying-a-directory"></a>
#### Копирование каталога

```markdown
C:\> xcopy /e "<PATH_FROM>" "<PATH_TO>"
```

где:

- `/e` - копирует все подкаталоги, даже если они пусты;
- `<PATH_FROM>` - путь до каталога, который необходимо скопировать;
- `<PATH_TO>` - путь до каталога, в который необходимо скопировать;

<a name="file-copy"></a>
#### Копирование файла

```markdown
C:\> copy /y "<PATH_FROM>\<FILE_FROM>" "<PATH_TO>\<FILE_TO>"
```

где:

- `/y` - подавляет запрос на подтверждение перезаписи существующего целевого файла;
- `<PATH_FROM>` - путь до каталога, из которого необходимо скопировать файл;
- `<FILE_FROM>` - имя копируемого файла;
- `<PATH_TO>` - путь до каталога, в которое необходимо скопировать файл;
- `<FILE_TO>` - новое имя файла (можно изменить при необходимости);

<a name="deleting-a-directory"></a>
#### Удаление каталога

```markdown
C:\> rmdir /s /q "<PATH>"
```

где:

- `/s` - удаляет дерево каталогов (указанный каталог и все его подкаталоги, включая все файлы);
- `/q` - тихий режим, не запрашивает подтверждение при удалении дерева каталогов. Параметр `/q` работает только при указании параметра `/s`;
- `<PATH>` - путь до каталога, включающий имя каталога, которую необходимо удалить;

<a name="symbolic-link-to-directory"></a>
#### Символическая ссылка на каталог

```markdown
C:\> mklink /j "<PATH_FROM>" "<PATH_TO>"
```

где:

- `/j` - создает соединение с каталогом;
- `<PATH_FROM>` - имя каталог или путь до каталога (включающий имя каталога) с символической ссылкой;
- `<PATH_TO>` - путь до каталога, куда ссылается символическая ссылка;

<a name="sources"></a>
## Источники

- [md (docs.microsoft.com)](https://docs.microsoft.com/ru-ru/windows-server/administration/windows-commands/md)
- [Как создать каталог (папку) в командной строке Windows 7 или Windows 10 (comp-security.net)](https://comp-security.net/%D0%BA%D0%B0%D0%BA-%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D1%82%D1%8C-%D0%BA%D0%B0%D1%82%D0%B0%D0%BB%D0%BE%D0%B3-%D0%BF%D0%B0%D0%BF%D0%BA%D1%83-%D0%B2-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BD%D0%BE%D0%B9/)
- [xcopy (docs.microsoft.com)](https://docs.microsoft.com/ru-ru/windows-server/administration/windows-commands/xcopy)
- [copy (docs.microsoft.com)](https://docs.microsoft.com/ru-ru/windows-server/administration/windows-commands/copy)
- [Как скопировать файл (папку) в командной строке Windows29.11.2021 (comp-security.net)](https://comp-security.net/%d0%ba%d0%b0%d0%ba-%d1%81%d0%ba%d0%be%d0%bf%d0%b8%d1%80%d0%be%d0%b2%d0%b0%d1%82%d1%8c-%d1%84%d0%b0%d0%b9%d0%bb-%d0%bf%d0%b0%d0%bf%d0%ba%d1%83-%d0%b2-cmd/)
- [rmdir (docs.microsoft.com)](https://docs.microsoft.com/ru-ru/windows-server/administration/windows-commands/rmdir)
- [Как удалить файл или папку через командную строку Windows09.12.2021 (comp-security.net)](https://comp-security.net/%D1%83%D0%B4%D0%B0%D0%BB%D0%B8%D1%82%D1%8C-%D1%84%D0%B0%D0%B9%D0%BB-%D1%87%D0%B5%D1%80%D0%B5%D0%B7-%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BD%D1%83%D1%8E-%D1%81%D1%82%D1%80%D0%BE%D0%BA%D1%83/)
- [mklink (docs.microsoft.com)](https://docs.microsoft.com/ru-ru/windows-server/administration/windows-commands/mklink)