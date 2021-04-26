[&larr;](readme.md "MySQL") Изменяем кодировку БД MySQL и таблиц из Win-1251 в UTF-8
------------------------------------------------------------------------------------

> Перед манипуляциями с базой данных не забываем сделать бекап.

#### Смена кодировки для базы данных

```mysql
ALTER DATABASE `<DB_NAME>` charset=utf8;
```

где:
 
- `<DB_NAME>` - наименование базы данных;

#### Смена кодировки для таблицы

```mysql
ALTER TABLE `<DB_NAME>`.`<TABLE_NAME>` CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;
```

где:
 
- `<DB_NAME>` - наименование базы данных;
- `<TABLE_NAME>` - наименование таблицы;

## <a name="sources"></a> Источники

- [Как изменить кодировку базы MySQL из Win-1251 в UTF-8? (mdex-nn.ru)](https://mdex-nn.ru/page/izmenit-mysql-codepage-1251-utf8.html)