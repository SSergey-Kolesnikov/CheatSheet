[&larr;](readme.md "1С-Битрикс") Показ свойства на детальной странице при создании его на API Битрикса
------------------------------------------------------------------------------------------------------

Для включения галочки "Показывать на детальной странице элемент" в настройках свойства инфоблока необходимо в список параметров передать массив к ключу `FEATURES`. К примеру:

```php
<?php
$arFields = [
   ...
   'FEATURES' => [
      [
         'IS_ENABLED' => 'Y',
         'MODULE_ID' => 'iblock',
         'FEATURE_ID' => 'DETAIL_PAGE_SHOW'
      ],
   ]
];

$ibp = new CIBlockProperty;
$PropID = $ibp->Add($arFields);
```

<a name="sources"></a>
## Источники

- [CIBlockProperty::Add (dev.1c-bitrix.ru)](https://dev.1c-bitrix.ru/api_help/iblock/classes/ciblockproperty/add.php)