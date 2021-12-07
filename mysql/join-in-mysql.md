[&larr;](readme.md "MySQL") JOIN в MySQL
----------------------------------------

<a name="content"></a>
## Содержание

- [Структура таблиц](#structure-of-tables)
    - [Таблица `universities`](#table-universities)
    - [Таблица `courses`](#table-courses)
    - [Таблица `students`](#table-students)
    - [Таблица `student_course`](#table-student-course)
- [INNER JOIN](#inner-join)
    - [Список университетов и их курсов](#list-of-universities-and-their-courses)
    - [Список студентов с их привязкой к университетам и курсам](#list-of-students-with-their-reference-to-universities-and-courses)
    - [Список самых популярных университетов](#list-of-the-most-popular-universities)
    - [Список самых популярных курсов у университетов](#list-of-the-most-popular-courses-at-universities)
- [Дамп базы данных](#database-dump)
- [Источники](#sources)

<a name="structure-of-tables"></a>
## Структура таблиц

<a name="table-universities"></a>
### Таблица `universities`

id | name
:---: | ---
1 | МГУ
2 | МФТИ
3 | МИФИ
4 | ВШЭ
5 | МГИМО
6 | МГТУ

<a name="table-courses"></a>
### Таблица `courses`

id | name | university_id
:---: | --- | :---:
1 | Основы сетевой безопасности | 1
2 | Управление инфраструктурой и развертывание облачных сервисов | 1
3 | Технология Блокчейн | 1
4 | Искусство разработки на современном C++ | 1
5 | Разработка интерфейсов: вёрстка и JavaScript | 1
6 | iOS-разработка: Swift, UI и многопоточность | 2
7 | Криптографические методы защиты информации | 3
8 | Антикризисная разработка корпоративных информационных систем | 3
9 | Человеческий фактор в разработке корпоративных систем | 4
10 | Алгоритмизация и программирование | 4
11 | Беспроводные коммуникационные системы | 4
12 | Введение в системы беспроводной связи | 5
13 | Цифровые технологии в международных финансах. Практикум | 5
14 | Платежные системы в цифровой экономике | 5
15 | Международные и национальные рейтинговые агентства | 5

<a name="table-students"></a>
### Таблица `students`

id | name
:---: | ---
1 | Никита
2 | Маша
3 | Ваня
4 | Даша
5 | Петя
6 | Света

<a name="table-student-course"></a>
### Таблица `student_course`

student_id | course_id
:---: | :---:
1 | 1
1 | 3
1 | 5
1 | 7
1 | 9
2 | 2
2 | 4
2 | 6
2 | 8
3 | 2
3 | 3
3 | 4
4 | 4
4 | 5
5 | 8

<a name="inner-join"></a>
## INNER JOIN

По умолчанию, если не указаны какие-либо параметры, JOIN выполняется как INNER JOIN, то есть как внутреннее (перекрёстное) соединение таблиц.

> Внутреннее соединение — соединение двух таблиц, при котором каждая запись из первой таблицы соединяется с каждой записью второй таблицы, создавая тем самым все возможные комбинации записей обеих таблиц (декартово произведение).

<a name="list-of-universities-and-their-courses"></a>
### Список университетов и их курсов

#### SQL-запрос

```sql
SELECT
  `universities`.`id` AS `university_id`,
  `universities`.`name` AS `university_name`,
  `courses`.`id` AS `course_id`,
  `courses`.`name` AS `course_name`
FROM
  `universities`
INNER JOIN
  `courses` ON `universities`.`id` = `courses`.`university_id`
ORDER BY
  `universities`.`id` ASC,
  `courses`.`id` ASC
```

#### Результат

university_id | university_name | course_id | course_name
:---: | --- | :---: | ---
1 | МГУ | 1 | Основы сетевой безопасности
1 | МГУ | 2 | Управление инфраструктурой и развертывание облачных сервисов
1 | МГУ | 3 | Технология Блокчейн
1 | МГУ | 4 | Искусство разработки на современном C++
1 | МГУ | 5 | Разработка интерфейсов: вёрстка и JavaScript
2 | МФТИ | 6 | iOS-разработка: Swift, UI и многопоточность
3 | МИФИ | 7 | Криптографические методы защиты информации
3 | МИФИ | 8 | Антикризисная разработка корпоративных информационных систем
3 | МИФИ | 9 | Человеческий фактор в разработке корпоративных систем
4 | ВШЭ | 10 | Алгоритмизация и программирование
4 | ВШЭ | 11 | Беспроводные коммуникационные системы
5 | МГИМО | 12 | Введение в системы беспроводной связи
5 | МГИМО | 13 | Цифровые технологии в международных финансах. Практикум
5 | МГИМО | 14 | Платежные системы в цифровой экономике
5 | МГИМО | 15 | Международные и национальные рейтинговые агентства

<a name="list-of-students-with-their-reference-to-universities-and-courses"></a>
### Список студентов с их привязкой к университетам и курсам 

#### SQL-запрос

```sql
SELECT
  `students`.`id` AS `student_id`,
  `students`.`name` AS `student_name`,
  `universities`.`id` AS `university_id`,
  `universities`.`name` AS `university_name`,
  `courses`.`id` AS `course_id`,
  `courses`.`name` AS `course_name`
FROM
  `universities`
INNER JOIN
  `courses` ON `universities`.`id` = `courses`.`university_id`
INNER JOIN
  `student_course` ON `courses`.`id` = `student_course`.`course_id`
INNER JOIN
  `students` ON `students`.`id` = `student_course`.`student_id`
ORDER BY
  `students`.`id` ASC,
  `universities`.`id` ASC,
  `courses`.`id` ASC
```

#### Результат

student_id | student_name | university_id | university_name | course_id | course_name
:---: | --- | :---: | --- | :---: | ---
1 | Никита | 1 | МГУ | 1 | Основы сетевой безопасности
1 | Никита | 1 | МГУ | 3 | Технология Блокчейн
1 | Никита | 1 | МГУ | 5 | Разработка интерфейсов: вёрстка и JavaScript
1 | Никита | 3 | МИФИ | 7 | Криптографические методы защиты информации
1 | Никита | 3 | МИФИ | 9 | Человеческий фактор в разработке корпоративных систем
2 | Маша | 1 | МГУ | 2 | Управление инфраструктурой и развертывание облачных сервисов
2 | Маша | 1 | МГУ | 4 | Искусство разработки на современном C++
2 | Маша | 2 | МФТИ | 6 | iOS-разработка: Swift, UI и многопоточность
2 | Маша | 3 | МИФИ | 8 | Антикризисная разработка корпоративных информационных систем
3 | Ваня | 1 | МГУ | 2 | Управление инфраструктурой и развертывание облачных сервисов
3 | Ваня | 1 | МГУ | 3 | Технология Блокчейн
3 | Ваня | 1 | МГУ | 4 | Искусство разработки на современном C++
4 | Даша | 1 | МГУ | 4 | Искусство разработки на современном C++
4 | Даша | 1 | МГУ | 5 | Разработка интерфейсов: вёрстка и JavaScript
5 | Петя | 3 | МИФИ | 8 | Антикризисная разработка корпоративных информационных систем

<a name="list-of-the-most-popular-universities"></a>
### Список самых популярных университетов 

#### SQL-запрос

```sql
SELECT
  `universities`.`id` AS `university_id`,
  `universities`.`name` AS `university_name`,
  COUNT(`students`.`id`) AS `students_count`
FROM
  `universities`
INNER JOIN
  `courses` ON `universities`.`id` = `courses`.`university_id`
INNER JOIN
  `student_course` ON `courses`.`id` = `student_course`.`course_id`
INNER JOIN
  `students` ON `students`.`id` = `student_course`.`student_id`
GROUP BY
  `universities`.`id`
ORDER BY
  `students_count` DESC,
  `universities`.`id` ASC
```

#### Результат

university_id | university_name | students_count
:---: | --- | :---:
1 | МГУ | 10
3 | МИФИ | 4
2 | МФТИ | 1


<a name="list-of-the-most-popular-courses-at-universities"></a>
### Список самых популярных курсов у университетов 

#### SQL-запрос

```sql
SELECT
  `courses`.`id` AS `course_id`,
  `courses`.`name` AS `course_name`,
  `universities`.`id` AS `university_id`,
  `universities`.`name` AS `university_name`,
  COUNT(`students`.`id`) AS `students_count`
FROM
  `universities`
INNER JOIN
  `courses` ON `universities`.`id` = `courses`.`university_id`
INNER JOIN
  `student_course` ON `courses`.`id` = `student_course`.`course_id`
INNER JOIN
  `students` ON `students`.`id` = `student_course`.`student_id`
GROUP BY
  `courses`.`id`
ORDER BY
  `students_count` DESC,
  `universities`.`id` ASC,
  `courses`.`id` ASC
```

#### Результат

course_id | course_name | university_id | university_name | students_count
:---: | --- | :---: | --- | :---:
4 | Искусство разработки на современном C++ | 1 | МГУ | 3
2 | Управление инфраструктурой и развертывание облачных сервисов | 1 | МГУ | 2
3 | Технология Блокчейн | 1 | МГУ | 2
5 | Разработка интерфейсов: вёрстка и JavaScript | 1 | МГУ | 2
8 | Антикризисная разработка корпоративных информационных систем | 3 | МИФИ | 2
1 | Основы сетевой безопасности | 1 | МГУ | 1
6 | iOS-разработка: Swift, UI и многопоточность | 2 | МФТИ | 1
7 | Криптографические методы защиты информации | 3 | МИФИ | 1
9 | Человеческий фактор в разработке корпоративных систем | 3 | МИФИ | 1

<a name="database-dump"></a>
## Дамп базы данных

<details>
<summary><i>Дамп базы данных</i></summary>

```sql
-- Отключение ограничения по внешнему ключу

SET FOREIGN_KEY_CHECKS=0;

-- --------------------------------------------------------

--
-- Структура таблицы `universities`
--

DROP TABLE IF EXISTS `universities`;
CREATE TABLE IF NOT EXISTS `universities` (
  `id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL DEFAULT '',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--
-- Дамп данных таблицы `universities`
--

INSERT INTO `universities` (`id`, `name`) VALUES
(1, 'МГУ'),
(2, 'МФТИ'),
(3, 'МИФИ'),
(4, 'ВШЭ'),
(5, 'МГИМО'),
(6, 'МГТУ');

-- --------------------------------------------------------

--
-- Структура таблицы `courses`
--

DROP TABLE IF EXISTS `courses`;
CREATE TABLE IF NOT EXISTS `courses` (
  `id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  `university_id` bigint(20) UNSIGNED DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `university_courses_id_foreign` (`university_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--
-- Дамп данных таблицы `courses`
--

INSERT INTO `courses` (`id`, `name`, `university_id`) VALUES
(1, 'Основы сетевой безопасности', 1),
(2, 'Управление инфраструктурой и развертывание облачных сервисов', 1),
(3, 'Технология Блокчейн', 1),
(4, 'Искусство разработки на современном C++', 1),
(5, 'Разработка интерфейсов: вёрстка и JavaScript', 1),
(6, 'iOS-разработка: Swift, UI и многопоточность', 2),
(7, 'Криптографические методы защиты информации', 3),
(8, 'Антикризисная разработка корпоративных информационных систем', 3),
(9, 'Человеческий фактор в разработке корпоративных систем', 3),
(10, 'Алгоритмизация и программирование', 4),
(11, 'Беспроводные коммуникационные системы', 4),
(12, 'Введение в системы беспроводной связи', 5),
(13, 'Цифровые технологии в международных финансах. Практикум', 5),
(14, 'Платежные системы в цифровой экономике', 5),
(15, 'Международные и национальные рейтинговые агентства', 5);

-- --------------------------------------------------------

--
-- Структура таблицы `students`
--

DROP TABLE IF EXISTS `students`;
CREATE TABLE IF NOT EXISTS `students` (
  `id` bigint(20) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` varchar(255) COLLATE utf8mb4_unicode_ci NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--
-- Дамп данных таблицы `students`
--

INSERT INTO `students` (`id`, `name`) VALUES
(1, 'Никита'),
(2, 'Маша'),
(3, 'Ваня'),
(4, 'Даша'),
(5, 'Петя'),
(6, 'Света');

-- --------------------------------------------------------

--
-- Структура таблицы `student_course`
--

DROP TABLE IF EXISTS `student_course`;
CREATE TABLE IF NOT EXISTS `student_course` (
  `student_id` bigint(20) UNSIGNED DEFAULT NULL,
  `course_id` bigint(20) UNSIGNED DEFAULT NULL,
  UNIQUE KEY (`student_id`,`course_id`),
  KEY `student_course_student_id_foreign` (`student_id`),
  KEY `student_course_course_id_foreign` (`course_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

--
-- Дамп данных таблицы `student_course`
--

INSERT INTO `student_course` (`student_id`, `course_id`) VALUES
(1, 1),
(1, 3),
(1, 5),
(1, 7),
(1, 9),
(2, 2),
(2, 4),
(2, 6),
(2, 8),
(3, 2),
(3, 3),
(3, 4),
(4, 4),
(4, 5),
(5, 8);

-- --------------------------------------------------------

--
-- Ограничения внешнего ключа сохраненных таблиц
--

--
-- Ограничения внешнего ключа таблицы `courses`
--
ALTER TABLE `courses`
  ADD CONSTRAINT `courses_universities_id_foreign` FOREIGN KEY (`university_id`) REFERENCES `universities` (`id`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- Ограничения внешнего ключа таблицы `student_course`
--
ALTER TABLE `student_course`
  ADD CONSTRAINT `student_course_student_id_foreign` FOREIGN KEY (`student_id`) REFERENCES `students` (`id`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `student_course_course_id_foreign` FOREIGN KEY (`course_id`) REFERENCES `courses` (`id`) ON DELETE CASCADE ON UPDATE CASCADE;

-- --------------------------------------------------------

-- Включение ограничения по внешнему ключу

SET FOREIGN_KEY_CHECKS=1;
```
</details>

<a name="sources"></a>
## Источники

- [SQL join в примерах с описанием (shra.ru)](https://shra.ru/2017/09/sql-join-v-primerakh-s-opisaniem/)
- [Многотабличные запросы, оператор JOIN (sql-academy.org)](https://sql-academy.org/ru/guide/multi-table-request-join)