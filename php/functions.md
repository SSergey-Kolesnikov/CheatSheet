[&larr;](readme.md "PHP") Функции
---------------------------------

## <a name="content"></a> Содержание:
- [Переменное число параметров функции](#functions_variable_number_of_function_parameters)
- [Типы аргументов и возвращаемого значения](#functions_types_of_arguments_and_return_value)
- [Строгая типизация](#functions_strong_typing)
- [Особенности инструкции global](#functions_features_of_the_global_instructionfunctions_features_of_the_global_instruction)
- [Статические переменные](#functions_static_variables)
- [Передача функций по ссылке](#functions_passing_functions_by_reference)
- [Замыкание](#functions_circuit)

#### <a name="functions_variable_number_of_function_parameters"></a> Переменное число параметров функции [&uarr;](#content "Содержание")
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 216 страница; pdf - 212 страница);

Для организации переменного числа параметров в функции, перед параметром может быть указано многоточие. Внутри функции такой параметр рассматривается как массив, содержащий все дополнительные параметры.

Листинг:

```markdown
function myecho(...$planets)
{
    foreach ($planets as $v) {
        echo "$v<br />\n"; // выводим элемент
    }
}
myecho("Меркурий", "Венера", "Земля", "Марс");
```

Вывод на экран:

```markdown
Меркурий
Венера
Земля
Марс
```

Оператор `...` может использоваться не только перед аргументами функций, но и при вызове с массивом. Это позволяет осуществить "развертывание" массива.

Листинг:

```markdown
function toomanyargs($fst, $snd, $thd, $fth)
{
    echo "Первый параметр: $fst<br />";
    echo "Второй параметр: $snd<br />";
    echo "Третий параметр: $thd<br />";
    echo "Четвертый параметр: $fth<br />";
}
$planets = ["Меркурий", "Венера", "Земля", "Марс"];
toomanyargs(...$planets);
```

Вывод на экран:

```markdown
Первый параметр: Меркурий
Второй параметр: Венера
Третий параметр: Земля
Четвертый параметр: Марс
```

### <a name="functions_types_of_arguments_and_return_value"></a> Типы аргументов и возвращаемого значения
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 217 страница; pdf - 213 страница);

```markdown
function sum(int $fst, int $snd): int
{
    return $fst + $snd;
}
echo sum(2, 2);
echo sum(2.5, 2.5); // Fatal Error в PHP < 7, Exception TypeError в PHP >=7
```

PHP автоматически приводит вещественный тип к целому. Для того чтобы PHP эмулировал режим жесткой типизации и требовал от аргументов функции указанные при объявлении типов, необходимо включить строгий режим типизации.

### <a name="functions_strong_typing"></a> Строгая типизация
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 218 страница; pdf - 214 страница);

```markdown
declare(strict_types=1);
function sum($fst, $snd): int
{
    return $fst + $snd;
}

echo sum(2, 2); // 4
echo sum(2.5, 2.5); // Fatal Error в PHP < 7, Exception TypeError в PHP >=7
```

До версии PHP7 использование неправильного типа в строгом режиме приводил к выдаче ошибки и остановке программы. Начиная с PHP7, вместо ошибки генерируется исключение `TypeError`, которое можно перехватить в программе.

### <a name="functions_features_of_the_global_instruction"></a> Особенности инструкции global
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 221 страница; pdf - 217 страница);

Листинг:

```markdown
$a = 100;
function test()
{ 
    global $a;
    unset($a);
}
test();
echo $a;
```

Вывод на экран:

```markdown
100
```

Т.е. настоящая `$a` не была удалена в `test()`! Для удаления глобальной переменной `$a` из функции необходимо:

```markdown
function deleter() { unset($GLOBALS['a']); }
$a = 100;
deleter();
echo $a;
```

В данном примере будет предупреждение, что переменная `$a` не определена!

### <a name="functions_static_variables"></a> Статические переменные
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 222 страница; pdf - 218 страница);

```markdown
function selfcount()
{
    static $count = 0;
    $count++;
    echo $count;
}
for ($i = 0; $i < 5; $i++) selfcount();
```

После запуска будет выведена строка `12345`, а если убрать statis - то `11111`.

### <a name="functions_passing_functions_by_reference"></a> Передача функций по ссылке
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 228 страница; pdf - 224 страница);

Листинг:

```markdown
function A($i) { echo "Вызвана A($i)<br />"; }
function B($i) { echo "Вызвана B($i)<br />"; }
function C($i) { echo "Вызвана C($i)<br />"; }
$F = "C";
$F(303);
call_user_func($F, 101);
call_user_func("B", 201);
```

Вывод на экран:

```markdown
Вызвана C(303)
Вызвана C(101)
Вызвана B(201)
```

### <a name="functions_circuit"></a> Замыкание
- Котеров Д., Симдянов И. - PHP 7 в подлиннике (ориг. - 230 страница; pdf - 226 страница);

Листинг:

```markdown
$message = "Работа не может быть продолжена из-за ошибок:<br />";
$check = function (array $errors) use ($message) {
    if (isset($errors) && count($errors) > 0) {
        echo $message;
        foreach ($errors as $error) {
            echo "$error<br />";
        }
    }
};
$check([]);
// ...
$erorrs[] = "Заполните имя пользователя";
$check($erorrs);
// ...
$message = "Список требований:"; // Уже не изменить
$erorrs = ["PHP", "MySQL", "memcache"];
$check($erorrs);
```

Вывод на экран:

```markdown
Работа не может быть продолжена из-за ошибок:
Заполните имя пользователя
Работа не может быть продолжена из-за ошибок:
PHP
MySQL
memcache
```

Листинг:

```markdown
$g = 'test';
$c = function($a, $b) use($g){
    echo $a . $b .  $g;
};
$g = 'test2';
echo "<pre>"; print_r($c);
```

Вывод на экран:

```markdown
Closure Object
(
    [static] => Array
        (
            [g] => test
        )
    [parameter] => Array
        (
            [$a] => 
            [$b] => 
        )
)
```