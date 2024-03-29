[&larr;](readme.md "Ubuntu") Установка драйвера Nvidia c Secure Boot на Ubuntu 20
---------------------------------------------------------------------------------

Для установки драйвера Nvidia на ОС Ubuntu c Secure Boot необходимо выполнить следующие действия:

- Открыть приложение "Программы и обновления", закладка "Дополнительные драйверы" и выбрать последнюю версию проприетарного драйвера;
- Во время установки проприетарного драйвера появится окно "Secure Boot" с предложением ввести пароль, придумываем и вводим пароль, далее он потребуется;
- После установки проприетарного драйвера перезагружаем компьютер;
- При загрузке компьютера появится окно программы MokManager, необходимо выбрать второй пункт "Enroll MOK" и указываем ранее введенный пароль;

После загрузки ОС проверяем в настройках использующийся драйвер, должен быть указан драйвера от Nvidia.

<a name="sources"></a>
## Источники

- [SecureBoot (wiki.ubuntu.com)](https://wiki.ubuntu.com/UEFI/SecureBoot)
- [Как поменять видеокарту по умолчанию в ubuntu на nvidia? (ru.stackoverflow.com)](https://ru.stackoverflow.com/questions/960944/%d0%9a%d0%b0%d0%ba-%d0%bf%d0%be%d0%bc%d0%b5%d0%bd%d1%8f%d1%82%d1%8c-%d0%b2%d0%b8%d0%b4%d0%b5%d0%be%d0%ba%d0%b0%d1%80%d1%82%d1%83-%d0%bf%d0%be-%d1%83%d0%bc%d0%be%d0%bb%d1%87%d0%b0%d0%bd%d0%b8%d1%8e-%d0%b2-ubuntu-%d0%bd%d0%b0-nvidia/961151#961151)
