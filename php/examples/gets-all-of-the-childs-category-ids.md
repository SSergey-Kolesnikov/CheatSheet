[&larr;](readme.md "Примеры") Получение идентификаторов дочерних категорий
--------------------------------------------------------------------------

Листинг:

```php
<?php
$categories = [
    ['id' => 1, 'parent' => 0],
    ['id' => 2, 'parent' => 0],
    ['id' => 3, 'parent' => 0],
    ['id' => 4, 'parent' => 2],
    ['id' => 5, 'parent' => 2],
    ['id' => 6, 'parent' => 1],
    ['id' => 7, 'parent' => 4],
    ['id' => 8, 'parent' => 7],
];

$ids = getChildIds(2, $categories);

/**
 * Gets all of the childs category ids for a given category.
 *
 * @param integer $id
 * @param array $categories
 * @param integer $depth
 *
 * @return array
 */
function getChildIds($id = null, array $categories = array(), $depth = 10) {
    $childrens = array();
    if ($id !== null && intval($depth) >= 1) {
        $id = is_int($id) ? $id : intval($id);
        if ($keys = array_keys(array_column($categories, 'parent'), $id)) {
            foreach ($keys as $key) {
                $childrens[] = $categories[$key]['id'];
                if ($subchildrens = getChildIds($categories[$key]['id'], $categories, $depth - 1)) {
                    $childrens = array_merge($childrens, $subchildrens);
                }
            }
        }
    }
    sort($childrens);
    return $childrens;
}
```

В переменной `$ids` будет содержаться:

```markdown
Array
(
    [0] => 4
    [1] => 5
    [2] => 7
    [3] => 8
)
```

Третьим параметром для функции `getChildIds` можно указать вложенность (по умолчанию = 10), к примеру единицу и тогда в переменной `$ids` будет содержаться:

```markdown
Array
(
    [0] => 4
    [1] => 5
)
```