[&larr;](readme.md "Windows") Установка принтера Xerox Phaser 3100MFP на Windows 10
-----------------------------------------------------------------------------------

Инструкция по установке и настройке принтера Xerox Phaser 3100MFP в Windows 10.

Официальных драйверов принтера Xerox Phaser 3100MFP под Windows 10 нет, поэтому будут использоваться драйвера других версий Windows.

1. Скачиваем [драйвера для Windows 7](https://www.support.xerox.com/en-us/product/phaser-3100mfp/downloads?language=en&platform=win7x64), а именно файл `XeroxCompanionSuite_V1_2_5UL.exe` и скачать его можно [тут](https://www.support.xerox.com/en-us/product/phaser-3100mfp/content/108767?language=en&platform=win7x64).

2. Запускаем установку драйверов и устанавливаем только драйвера для принтера без приложений. В итоге после установки драйвера принтер будет работать, но сканер еще работать не будет.

3. Теперь скачиваем [драйвера для Windows 8](https://www.support.xerox.com/en-us/product/phaser-3100mfp/downloads?language=en&platform=win81x64), а именно файл `PH3100_x64_v11.0.1.17.zip` и скачать его можно [тут](https://www.support.xerox.com/en-us/product/phaser-3100mfp/content/127601?language=en&platform=win81x64).

4. Распаковываем архив и в последующем нам понадобится файл `WIALFFV2SCN.dll`.

5. Теперь необходимо остановить службу загрузки изображений в Windows. Для этого открываем список служб с помощью команды `services.msc`, находим службу `Служба загрузки изображений Windows (WIA)` и останавливаем ее.

6. Копируем файл `WIALFFV2SCN.dll` из архива `PH3100_x64_v11.0.1.17.zip` в папку `C:\Windows\System32` с заменой существующего файла.

7. И в конце необходимо запустить службу загрузки изображений в Windows. В списке служб находим ранее остановленную службу `Служба загрузки изображений Windows (WIA)` и запускаем ее.

На этом все, теперь принтер и сканер должны работать в Windows 10.

<a name="sources"></a>
## Источники

- [Установка принтера Xerox Phaser 3100MFP на Windows 10 (internet-lab.ru)](https://internet-lab.ru/xerox_phaser_3100mfp_win10)