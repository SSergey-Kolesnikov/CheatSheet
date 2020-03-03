[&larr;](readme.md "PHP") Операторы
-----------------------------------

## <a name="content"></a> Содержание:
- [Null-коалесцентный оператор](#operators_null_coalesce_op)
- [Оператор "космический корабль"](#operators_spaceship_op)

#### <a name="operators_null_coalesce_op"></a> Null-коалесцентный оператор [&uarr;](#content "Содержание")
- [Тернарный оператор (php.net)](https://www.php.net/manual/ru/language.operators.comparison.php#language.operators.comparison.ternary)
- [Оператор объединения с null (php.net)](https://www.php.net/manual/ru/migration70.new-features.php#migration70.new-features.null-coalesce-op)
- [Введение в PHP 7: Что добавлено, что убрано (habr.com)](https://habr.com/ru/post/280071/)

Решает распространенную проблему в PHP. Она возникает в случае, если мы хотим присвоить значение переменной, которое присвоено другой переменной, но если последней переменной значение не было присвоено, то присвоить некое явное значение.

##### До PHP 7:

Присваиваем `$bar` значение 'default' если `$foo` равен NULL

```markdown
if (isset($foo))
    $bar = $foo;
else
    $bar = 'default';
```

или

```markdown
if (isset($foo)) ? $bar = $foo : $bar = 'default';
```

##### В PHP 7:

```markdown
$bar = $foo ?? 'default';
```

или можно использовать с цепочкой переменных

```markdown
$bar = $foo ?? $baz ?? 'default';
```

### <a name="operators_spaceship_op"></a> Оператор "космический корабль" [&uarr;](#content "Содержание")
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 162 страница; pdf - 158 страница);
- [Оператор spaceship (космический корабль) (php.net)](https://www.php.net/manual/ru/migration70.new-features.php#migration70.new-features.spaceship-op)
- [Введение в PHP 7: Что добавлено, что убрано (habr.com)](https://habr.com/ru/post/280071/)

Оператор “космический корабль” <=> позволяет проводить трехуровневое сравнение двух значений, позволяя понимать не только их равенство или неравенство, но и то, которое из них больше при неравенстве, возвращая 1,0 или -1.

```markdown
switch ($bar <=> $foo) {
    case 0:
        echo '$bar и $foo равны';
    case -1:
        echo '$foo больше';
    case 1:
        echo '$bar больше';
}
```
