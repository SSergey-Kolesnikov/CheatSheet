[&larr;](readme.md "Примеры") Декартово произведение множеств в PHP
-------------------------------------------------------------------

> Декартово произведение множеств — множество, элементами которого являются все возможные упорядоченные пары элементов исходных множеств.

## <a name="content"></a> Содержание:

- [PHP Cartesian Function](#php-cartesian-function)
- [Библиотека `Hoa\Math`](#library-hoa-math)
- [Библиотека `cartesian-iterator`](#library-cartesian-iterator)
- [Источники](#sources)

## <a name="php-cartesian-function"></a> PHP Cartesian Function [&uarr;](#content "Содержание")

### Создаем PHP скрипт

```php
<?php

$attributeValues = [
    'color' => ['Red', 'White', 'Blue'],
    'size' => [1, 2, 3, 4],
    'fabric' => ['Cloth', 'Silk']
];

class Cartesian
{
    public static function build($set)
    {
        if (!$set) {
            return array([]);
        }

        $subset = array_shift($set);
        $cartesianSubset = self::build($set);

        $result = [];
        foreach ($subset as $value) {
            foreach ($cartesianSubset as $p) {
                array_unshift($p, $value);
                $result[] = $p;
            }
        }

        return $result;        
    }
}

print_r(Cartesian::build($attributeValues));
```

### Результаты выполнения PHP скрипта

```markdown
Array
(
    [0] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Cloth
        )

    [1] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Silk
        )

    [2] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Cloth
        )

    [3] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Silk
        )

    [4] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Cloth
        )

    [5] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Silk
        )

    [6] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Cloth
        )

    [7] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Silk
        )

    [8] => Array
        (
            [0] => White
            [1] => 1
            [2] => Cloth
        )

    [9] => Array
        (
            [0] => White
            [1] => 1
            [2] => Silk
        )

    [10] => Array
        (
            [0] => White
            [1] => 2
            [2] => Cloth
        )

    [11] => Array
        (
            [0] => White
            [1] => 2
            [2] => Silk
        )

    [12] => Array
        (
            [0] => White
            [1] => 3
            [2] => Cloth
        )

    [13] => Array
        (
            [0] => White
            [1] => 3
            [2] => Silk
        )

    [14] => Array
        (
            [0] => White
            [1] => 4
            [2] => Cloth
        )

    [15] => Array
        (
            [0] => White
            [1] => 4
            [2] => Silk
        )

    [16] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Cloth
        )

    [17] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Silk
        )

    [18] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Cloth
        )

    [19] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Silk
        )

    [20] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Cloth
        )

    [21] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Silk
        )

    [22] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Cloth
        )

    [23] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Silk
        )

)
```

## <a name="library-hoa-math"></a> Библиотека `Hoa\Math` [&uarr;](#content "Содержание")

Репозиторий: [hoaproject / Math](https://github.com/hoaproject/Math/).

> This library provides tools around mathematical operations.

### Устанавливаем библиотеку `Hoa\Math`

```markdown
user@computer:~$ composer require hoa/math '~1.0'
./composer.json has been created
Running composer update hoa/math
Loading composer repositories with package information
Updating dependencies
...
Generating autoload files
```

### Создаем PHP скрипт

```php
<?php

use Hoa\Math\Combinatorics\Combination\CartesianProduct;

require 'vendor/autoload.php';

$items = new CartesianProduct(
    ['Red', 'White', 'Blue'],
    [1, 2, 3, 4],
    ['Cloth', 'Silk']
);

$result = [];
foreach ($items as $item)
	$result[] = $item;

print_r($result);
```

### Результаты выполнения PHP скрипта

```markdown
Array
(
    [0] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Cloth
        )

    [1] => Array
        (
            [0] => White
            [1] => 1
            [2] => Cloth
        )

    [2] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Cloth
        )

    [3] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Cloth
        )

    [4] => Array
        (
            [0] => White
            [1] => 2
            [2] => Cloth
        )

    [5] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Cloth
        )

    [6] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Cloth
        )

    [7] => Array
        (
            [0] => White
            [1] => 3
            [2] => Cloth
        )

    [8] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Cloth
        )

    [9] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Cloth
        )

    [10] => Array
        (
            [0] => White
            [1] => 4
            [2] => Cloth
        )

    [11] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Cloth
        )

    [12] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Silk
        )

    [13] => Array
        (
            [0] => White
            [1] => 1
            [2] => Silk
        )

    [14] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Silk
        )

    [15] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Silk
        )

    [16] => Array
        (
            [0] => White
            [1] => 2
            [2] => Silk
        )

    [17] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Silk
        )

    [18] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Silk
        )

    [19] => Array
        (
            [0] => White
            [1] => 3
            [2] => Silk
        )

    [20] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Silk
        )

    [21] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Silk
        )

    [22] => Array
        (
            [0] => White
            [1] => 4
            [2] => Silk
        )

    [23] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Silk
        )

)
```

## <a name="library-cartesian-iterator"></a> Библиотека `cartesian-iterator` [&uarr;](#content "Содержание")

Репозиторий: [PatchRanger / cartesian-iterator](https://github.com/PatchRanger/cartesian-iterator).

> Iterator, returning the cartesian product of associative array of iterators.

### Устанавливаем библиотеку `cartesian-iterator`

```markdown
user@computer:~$ composer require patchranger/cartesian-iterator
Using version ^0.07.0 for patchranger/cartesian-iterator
./composer.json has been created
Running composer update patchranger/cartesian-iterator
Loading composer repositories with package information
Updating dependencies
...
Generating autoload files
```

### Создаем PHP скрипт

```php
<?php

use PatchRanger\CartesianIterator;

require 'vendor/autoload.php';

$cartesianIterator = new CartesianIterator();

$cartesianIterator->attachIterator(new ArrayIterator(['Red', 'White', 'Blue']));
$cartesianIterator->attachIterator(new ArrayIterator([1, 2, 3, 4]));
$cartesianIterator->attachIterator(new ArrayIterator(['Cloth', 'Silk']));

$result = iterator_to_array($cartesianIterator);

print_r($result);
```

### Результаты выполнения PHP скрипта

```markdown
Array
(
    [0] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Cloth
        )

    [1] => Array
        (
            [0] => White
            [1] => 1
            [2] => Cloth
        )

    [2] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Cloth
        )

    [3] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Cloth
        )

    [4] => Array
        (
            [0] => White
            [1] => 2
            [2] => Cloth
        )

    [5] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Cloth
        )

    [6] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Cloth
        )

    [7] => Array
        (
            [0] => White
            [1] => 3
            [2] => Cloth
        )

    [8] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Cloth
        )

    [9] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Cloth
        )

    [10] => Array
        (
            [0] => White
            [1] => 4
            [2] => Cloth
        )

    [11] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Cloth
        )

    [12] => Array
        (
            [0] => Red
            [1] => 1
            [2] => Silk
        )

    [13] => Array
        (
            [0] => White
            [1] => 1
            [2] => Silk
        )

    [14] => Array
        (
            [0] => Blue
            [1] => 1
            [2] => Silk
        )

    [15] => Array
        (
            [0] => Red
            [1] => 2
            [2] => Silk
        )

    [16] => Array
        (
            [0] => White
            [1] => 2
            [2] => Silk
        )

    [17] => Array
        (
            [0] => Blue
            [1] => 2
            [2] => Silk
        )

    [18] => Array
        (
            [0] => Red
            [1] => 3
            [2] => Silk
        )

    [19] => Array
        (
            [0] => White
            [1] => 3
            [2] => Silk
        )

    [20] => Array
        (
            [0] => Blue
            [1] => 3
            [2] => Silk
        )

    [21] => Array
        (
            [0] => Red
            [1] => 4
            [2] => Silk
        )

    [22] => Array
        (
            [0] => White
            [1] => 4
            [2] => Silk
        )

    [23] => Array
        (
            [0] => Blue
            [1] => 4
            [2] => Silk
        )

)
```

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [PHP Cartesian Function (gist.github.com)](https://gist.github.com/jwage/11193216)
- [hoaproject / Math (github.com)](https://github.com/hoaproject/Math/)
- [PatchRanger / cartesian-iterator (github.com)](https://github.com/PatchRanger/cartesian-iterator)