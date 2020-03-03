[&larr;](readme.md "Примеры") Преобразование секунд в секунды/минуты/часы
-------------------------------------------------------------------------

#### Вывод времени без учета нулевых значений

Листинг:

```php
<?php
$seconds = array(5, 10, 123, 456, 789, 1234, 5678, 9012, 12345, 67890, 123456);

foreach ($seconds as $second) {
    echo $second . ' сек. = ' . seconds2times($second) . '<br />';
}

/**
 * Convert seconds to seconds/minutes/hours
 *
 * @param int $seconds
 * @param bool $count_zero
 *
 * @return string $output:
 */
function seconds2times($seconds, $count_zero = false) {
    $output = '';
    $periods = array(60, 3600);
    $times_values = array('сек.', 'мин.', 'час.');

    for ($i = 1; $i >= 0; $i--) {
        $period = floor($seconds / $periods[$i]);
        if (($period > 0) || ($period == 0 && $count_zero)) {
            $times[$i + 1] = $period;
            $seconds -= $period * $periods[$i];
            $count_zero = true;
        }
    }
    $times[0] = $seconds;

    for ($i = count($times) - 1; $i >= 0; $i--) {
        $output .= $times[$i] . $times_values[$i] . ' ';
    }

    return trim($output);
}
```

Вывод на экран:

```markdown
5 сек. = 5сек.
10 сек. = 10сек.
123 сек. = 2мин. 3сек.
456 сек. = 7мин. 36сек.
789 сек. = 13мин. 9сек.
1234 сек. = 20мин. 34сек.
5678 сек. = 1час. 34мин. 38сек.
9012 сек. = 2час. 30мин. 12сек.
12345 сек. = 3час. 25мин. 45сек.
67890 сек. = 18час. 51мин. 30сек.
123456 сек. = 34час. 17мин. 36сек.
```

#### Вывод времени с учетом нулевых значений

Листинг:

```php
<?php
$seconds = array(5, 10, 123, 456, 789, 1234, 5678, 9012, 12345, 67890, 123456);

foreach ($seconds as $second) {
    echo $second . ' сек. = ' . seconds2times($second, true) . '<br />';
}

/**
 * Convert seconds to seconds/minutes/hours
 *
 * @param int $seconds
 * @param bool $count_zero
 *
 * @return string $output:
 */
function seconds2times($seconds, $count_zero = false) {
    $output = '';
    $periods = array(60, 3600);
    $times_values = array('сек.', 'мин.', 'час.');

    for ($i = 1; $i >= 0; $i--) {
        $period = floor($seconds / $periods[$i]);
        if (($period > 0) || ($period == 0 && $count_zero)) {
            $times[$i + 1] = $period;
            $seconds -= $period * $periods[$i];
            $count_zero = true;
        }
    }
    $times[0] = $seconds;

    for ($i = count($times) - 1; $i >= 0; $i--) {
        $output .= $times[$i] . $times_values[$i] . ' ';
    }

    return trim($output);
}
```

Вывод на экран:

```markdown
5 сек. = 0час. 0мин. 5сек.
10 сек. = 0час. 0мин. 10сек.
123 сек. = 0час. 2мин. 3сек.
456 сек. = 0час. 7мин. 36сек.
789 сек. = 0час. 13мин. 9сек.
1234 сек. = 0час. 20мин. 34сек.
5678 сек. = 1час. 34мин. 38сек.
9012 сек. = 2час. 30мин. 12сек.
12345 сек. = 3час. 25мин. 45сек.
67890 сек. = 18час. 51мин. 30сек.
123456 сек. = 34час. 17мин. 36сек.
```

### Источник

- [Секунды в дни-часы-минуты (PHP) (expange.ru)](https://expange.ru/e/Секунды_в_дни-часы-минуты_(PHP))