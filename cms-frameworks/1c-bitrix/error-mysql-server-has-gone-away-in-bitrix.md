[&larr;](readme.md "1С-Битрикс") Ошибка "MySQL server has gone away" в Битрикс
------------------------------------------------------------------------------

Ошибка "MySQL server has gone away" может возникнуть при синхронизации с 1С, резервном копировании, выгрузках из CSV и т.п. Она говорит о том, что в процессе выполнения запроса сервер оборвал соединение. Проблема связана с настройкой MySQL и часто возникает, когда на сервере установлен небольшой лимит времени на соединение.

Вариантов решения этой проблемы может быть несколько, ниже несколько из них.

## <a name="content"></a> Содержание:

- [Установка таймаута из Битрикса](#setting-a-timeout-from-bitrix)
- [Добавление или увеличение размера swap-файла](#add-or-increase-swap-file-size)
- [Источники](#sources)

## <a name="setting-a-timeout-from-bitrix"></a> Установка таймаута из Битрикса [&uarr;](#content "Содержание")

В файле `/bitrix/php_interface/after_connect.php` добавляется строка:

```php
$DB->Query("SET wait_timeout=28800");
```

В файле `/bitrix/php_interface/after_connect_d7.php` добавляется строка:

```php
$connection->queryExecute("SET wait_timeout=28800");
```

Время, сколько сервер будет ждать активности соединения прежде, чем закрыть соединение - указывается в секундах, в нашем примере это 8 часов (максимально возможное значение).

## <a name="add-or-increase-swap-file-size"></a> Добавление или увеличение размера swap-файла [&uarr;](#content "Содержание")

С помощью команды `swapon -s` проверяем, имеется ли swap-файл:

```markdown
[root@localhost ~]# swapon -s
[root@localhost ~]# 
```

В данном примере swap-файл отсутствует.

```markdown
[root@localhost ~]# swapon -s
Filename                                Type            Size    Used    Priority
/swapfile                               file    2097148 736512  -2
[root@localhost ~]#
```

А в данном примере есть swap-файл на 2Гб. 

Далее с помощью команды `df -h /` проверяем количество свободного места на диске:

```markdown
[root@localhost ~]# df -h /
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        40G   27G   12G  70% /
[root@localhost ~]#
```

В данном примере свободно 12Гб.

Далее с помощью команды `dd if=/dev/zero of=/swapfile bs=1M count=2048` создаем swap-файл:

```markdown
[root@localhost ~]# dd if=/dev/zero of=/swapfile bs=1M count=2048
2048+0 records in
2048+0 records out
2147483648 bytes (2.1 GB) copied, 4.2405 s, 506 MB/s
[root@localhost ~]#
```

В данном примере размер создаваего блока равен 1Мб, а их количество будет 2048. В итоге размер создаваемого swap-файла будет 2Гб.

Далее проверяем права доступа к файлу с помощью команды `ls -alh /swapfile`:

```markdown
[root@localhost ~]# ls -alh /swapfile
-rw-r--r-- 1 root root 2.0G Oct 18 10:17 /swapfile
[root@localhost ~]#
```

В нашем примере права на файл "644", что не безопасно и он может быть прочтен еще кем-либо, помимо root-пользователя.

Далее с помощью команды `chmod 600 /swapfile` меняем права доступа к созданному swap-файлу на "600":

```markdown
[root@localhost ~]# chmod 600 /swapfile
[root@localhost ~]#
```

Теперь, если проверить права доступа к файлу командой `ls -alh /swapfile`, то увидим, что он доступен лишь root-пользователю:

```markdown
[root@localhost ~]# ls -alh /swapfile
-rw------- 1 root root 2.0G Oct 18 10:17 /swapfile
[root@localhost ~]#
```

Теперь с помощью команды `mkswap /swapfile` создаем пространство подкачки:

```markdown
[root@localhost ~]# mkswap /swapfile
Setting up swapspace version 1, size = 2097148 KiB
no label, UUID=ac8d4cc6-f43f-3259-b4b3-6d8e6b9e4f71
[root@localhost ~]#
```

Далее с помощью команды `swapon /swapfile` включаем swap-файл:

```markdown
[root@localhost ~]# swapon /swapfile
[root@localhost ~]#
```

И с помощью команды `swapon -s` проверяем, все ли правильно выполнено:

```markdown
[root@localhost ~]# swapon -s
Filename                                Type            Size    Used    Priority
/swapfile                               file    2097148 0       -2
[root@localhost ~]#
```

Swap-файл уже работает, но работать он будет до первой перезагрузки сервера и чтобы не включать его вручную при каждой перезагрузке сервера - добавляем запись о нем в файле `/etc/fstab`. В любом текстовом редакторе добавляем в конец файла `/etc/fstab` строку:

```markdown
/swapfile none swap sw 0 0
```

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [MySQL server has gone away - решение проблемы, один из вариантов (dev.1c-bitrix.ru)](https://dev.1c-bitrix.ru/community/webdev/user/94272/blog/11593/)
- [Подключение Swap-раздела (dev.1c-bitrix.ru)](https://dev.1c-bitrix.ru/learning/course/index.php?COURSE_ID=37&LESSON_ID=8889)
- [Добавить Swap в CentOS/Fedora/RedHat (linux-notes.org)](https://linux-notes.org/dobavit-swap-v-centos-fedora-redhat/)
- [Swap CentOS — подключение файла подкачки, удаление файла подкачки (i-notes.org)](https://i-notes.org/swap-centos-podklyuchenie-fajla-podkachki-udalenie-fajla-podkachki/)
- [КАК ДОБАВИТЬ СВОП НА CENTOS 7 (8host.com)](https://www.8host.com/blog/kak-dobavit-swap-na-centos-7/)
- [Bitrix VM увеличиваем размер swap (zen.yandex.ru)](https://zen.yandex.ru/media/id/5c236da11fdf2500aa89d901/bitrix-vm-uvelichivaem-razmer-swap-5c3f295140e8e300aa0a76bf)