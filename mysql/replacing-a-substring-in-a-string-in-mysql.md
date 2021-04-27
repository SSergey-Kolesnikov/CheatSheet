[&larr;](readme.md "MySQL") Замена подстроки в строке в MySQL
-------------------------------------------------------------

> Перед манипуляциями с базой данных не забываем сделать бекап.

```mysql
UPDATE `<TABLE_NAME>` SET `<FIELD_NAME>` = REPLACE(`<FIELD_NAME>`, '<FROM_SUBSTRING>', '<TO_SUBSTRING>');
```

где:

- `<TABLE_NAME>` - наименование таблицы;
- `<FIELD_NAME>` - наименование столбца;
- `<FROM_SUBSTRING>` - подстрока для поиска;
- `<TO_SUBSTRING>` - замещающая подстрока;

## <a name="sources"></a> Источники

- [Замена подстроки в строке в MySQL (coder-diary.ru)](http://coder-diary.ru/programming/zamena-podstroki-v-stroke-v-mysql/)
- [MySQL функция REPLACE (oracleplsql.ru)](https://oracleplsql.ru/mysql-function-replace.html)