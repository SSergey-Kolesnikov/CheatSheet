[&larr;](readme.md "MySQL") Выборка значений из диапазона с помощью BETWEEN в MySQL
-----------------------------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Синтаксис](#syntax)
- [Структура таблиц](#structure-of-tables)
    - [Таблица `products`](#table-products)
- [Примеры](#examples)
    - [Получить товары с ценой больше или равно 25 рублей и меньше или равно 75 рублей](#example-1)
- [Дамп базы данных](#database-dump)
- [Источники](#sources)

<a name="syntax"></a>
## Синтаксис

```mysql
<EXPR> BETWEEN <MIN> AND <MAX>
```

где:

- `<EXPR>` - столбец или расчет;
- `<MIN>` и `<MAX>` - диапазон;

<a name="structure-of-tables"></a>
## Структура таблиц

<a name="table-products"></a>
### Таблица `products`

id | name | price
:---: | --- | :---:
1 | Товар 1 | 10.86
2 | Товар 2 | 68.42
3 | Товар 3 | 95.34
4 | Товар 4 | 26.65
5 | Товар 5 | 35.27

<a name="examples"></a>
## Примеры

<a name="example-1"></a>
### Получить товары с ценой больше или равно 25 рублей и меньше или равно 75 рублей

#### SQL-запрос

```mysql
SELECT
  *
FROM
  `products`
WHERE
  `price` BETWEEN 25 AND 75
```

#### Результат

id | name | price
:---: | --- | :---:
2 | Товар 2 | 68.42
4 | Товар 4 | 26.65
5 | Товар 5 | 35.27

<a name="database-dump"></a>
## Дамп базы данных

<details>
<summary><i>Дамп базы данных</i></summary>

```sql
--
-- Структура таблицы `products`
--

DROP TABLE IF EXISTS `products`;
CREATE TABLE IF NOT EXISTS `products` (
  `id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL DEFAULT '',
  `price` decimal(18,2) UNSIGNED DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `products_price_index` (`price`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--
-- Дамп данных таблицы `products`
--

INSERT INTO `products` (`id`, `name`, `price`) VALUES
(1, 'Товар 1', '10.86'),
(2, 'Товар 2', '68.42'),
(3, 'Товар 3', '95.34'),
(4, 'Товар 4', '26.65'),
(5, 'Товар 5', '35.27');
```
</details>

<a name="sources"></a>
## Источники

- [12.4.2 Comparison Functions and Operators (dev.mysql.com)](https://dev.mysql.com/doc/refman/8.0/en/comparison-operators.html#operator_between)
- [Команда BETWEEN (old.code.)](http://old.code.mu/sql/between.html)