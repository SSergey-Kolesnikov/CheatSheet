[&larr;](readme.md "Примеры") Получение идентификаторов родительских категорий
------------------------------------------------------------------------------

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

$ids = getParentIds(8, $categories);

/**
 * Gets all of the parent category ids for a given category.
 *
 * @param integer $id
 * @param array $categories
 * @param integer $height
 * @return array
 */
function getParentIds($id = null, array $categories = array(), $height = 10) {
    $parents = array();
    if ($id !== null && intval($height) >= 1) {
        $id = is_int($id) ? $id : intval($id);
        if (array_search($id, array_column($categories, 'id')) !== false) {
            $key = array_search($id, array_column($categories, 'id'));
            if ($categories[$key]['parent'] && !empty($categories[$key]['parent'])) {
                $parents[] = $categories[$key]['parent'];
                if ($overparents = getParentIds($categories[$key]['parent'], $categories, $height - 1)) {
                    $parents = array_merge($parents, $overparents);
                }
            }
        }
    }
    return $parents;
}
```

В переменной `$ids` будет содержаться:

```markdown
Array
(
    [0] => 7
    [1] => 4
    [2] => 2
)
```

Третьим параметром для функции `getParentIds` можно указать вложенность (по умолчанию = 10), к примеру единицу и тогда в переменной `$ids` будет содержаться:

```markdown
Array
(
    [0] => 7
)
```