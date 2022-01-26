[&larr;](readme.md "Windows") Ошибка "Certificate used to sign the license is not signed JetBrains root certificate" при активации PhpStorm 2020.1
--------------------------------------------------------------------------------------------------------------------------------------------------

Переходим в папку `C:\Users\<USER>\AppData\Roaming\JetBrains\PhpStorm2020.1`, где `<USER>` - имя пользователя в Windows, находим файл `phpstorm64.exe.vmoptions`, открываем его в редакторе и удаляем все строки, связанные с `-javaagent`. После сохранения изменений лицензия активируется без ошибок.

<a name="sources"></a>
## Источники

- [Certificate used to sign the license is not signed by JetBrains root certificate (youtrack.jetbrains.com)](https://youtrack.jetbrains.com/issue/WEB-38698)
- [Certificate used to sign the license is not signed by JetBrains root (programmersought.com)](https://programmersought.com/article/35544133250/)