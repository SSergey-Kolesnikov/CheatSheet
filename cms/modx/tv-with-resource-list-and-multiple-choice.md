[&larr;](readme.md "MODX") TV со списком ресурсов и возможностью множественного выбора
--------------------------------------------------------------------------------------

Настройка TV в MODX для создания выпадающего списка ресурсов с возможностью множественного выбора.

#### Параметры ввода

Наименование | Значение
--- | ---
Тип ввода | Список (множественный выбор)
Возможные значения | @SELECT \`pagetitle\`, \`id\` FROM \`modx_site_content\` ORDER BY \`pagetitle\` ASC

В поле "Возможные значения" указывается SQL код для запроса в базу данных.

#### Параметры вывода

Наименование | Значение
--- | ---
Тип вывода | Разделитель
Разделитель | ,

## Источники

- [Cоздание списка TV c множественны выбором Ресурсов (modx.cc)](https://modx.cc/article/create-a-list-of-tv-c-multiple-choice-resources/)
- [Template Variable Input Types (docs.modx.com)](https://docs.modx.com/current/en/building-sites/elements/template-variables/input-types#more-advanced-usage)