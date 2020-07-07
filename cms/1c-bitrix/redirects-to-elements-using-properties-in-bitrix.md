[&larr;](readme.md "1С-Битрикс") Редиректы для элементов с использованием свойств в Битриксе
--------------------------------------------------------------------------------------------

Настройка редиректов для элементов со старого урла, хранящегося в отдельном свойстве, на новый урл с возможностью сохранения определенных GET-параметров. Удобно в случае изменения структуры сайта или при разработке нового сайта на основании уже имеющегося.

Первым делом создается текстовое свойство у элемента, где будет храниться старый урл. К примеру назовем его `OLD_URL` (пусть будет совпадать с символьным кодом), в дальнейшем понадобится код свойства. Формат урла: `/category/subcategory/product/`, т.е. урл начинается со слэша и без указания домена.

Далее необходимо подключить файл редиректов в файле `/bitrix/header.php` добавлением строки:

```php
include_once($_SERVER["DOCUMENT_ROOT"] . "/local/redirects.php");
```

Теперь в папке `/local/` создаем файл `redirects.php`:

```php
<?php
require_once($_SERVER["DOCUMENT_ROOT"] . "/bitrix/modules/main/include/prolog_before.php");

CModule::IncludeModule('iblock');

$savingParams = [];
$savedParams = [];

$request = Bitrix\Main\Context::getCurrent()->getRequest();
$oldUri = new Bitrix\Main\Web\Uri($request->getDecodedUri());

foreach ($savingParams as $savingParam) {
    $savedParams[$savingParam] = $request->getQuery($savingParam);
}
$oldUri->deleteParams($savingParams);

$rsItems = CIBlockElement::GetList(
    [],
    [
        "IBLOCK_ID" => [1,2,5,14],
        "ACTIVE" => "Y",
        "!CODE" => false,
        "PROPERTY_OLD_URL" => $oldUri->getPath()
    ],
    false,
    false,
    ["ID", "DETAIL_PAGE_URL"]
);
if ($rsItems->SelectedRowsCount() == 1 && $arItem = $rsItems->GetNext()) {
    $newUri = new Bitrix\Main\Web\Uri($arItem["DETAIL_PAGE_URL"]);
    $newUri->addParams(array_filter($savedParams));
    LocalRedirect($newUri->getUri(), false, 301);
    exit();
}
```

В переменной `$savingParams` можно указать список GET-параметров, которые необходимо сохранить. У ключа `IBLOCK_ID` в значении указывается список ID инфоблоков, в свойствах которых будет искаться старый урл. И в ключе `PROPERTY_OLD_URL` как раз указывается символьный код свойства, где хранится старый урл элемента.