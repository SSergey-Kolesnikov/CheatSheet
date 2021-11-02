[&larr;](../readme.md "Шпаргалка") SSH команды
----------------------------------------------

## <a name="content"></a> Содержание:

- [Apache](apache.md)
- [Composer](composer.md)
- [Cron](cron.md)
- [Git](git.md)
- [Midnight Commander](midnight-commander.md)
- [MySQL](mysql.md)
- [PHP](php.md)
- [Samba](samba.md)
- [Архиваторы](archivers.md)
- [Мониторинг работы системы, нагрузки сервера, сети и т.п.](monitoring-system-operation-server-load-network-etc.md)
- [Пользователи и группы пользователей](users-and-user-groups.md)
- [Файловая система](file-system.md)
- [Прочие команды](#other-commands)
- [Источник](#source)

## <a name="other-commands"></a> Прочие команды [&uarr;](#content "Содержание")

#### Название ОС

```markdown
uname -a
```

#### Перезагрузка компьютера

```markdown
shutdown -r now
```

#### Выключение компьютера

```markdown
shutdown -P now
```

#### Локальный IP адрес

```markdown
user@computer:~$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65563 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp2t7:: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    link/ether 00:e1:51:53:e0:ea brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.101/24 brd 192.168.1.255 scope global enp2t7:
       valid_lft forever preferred_lft forever
    inet6 fe75::2a0:35ee:ff65:ae/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s10: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 04:00:9c:61:c2:a0 brd ff:ff:ff:ff:ff:ff
```

#### Текущие дата/время

```markdown
user@computer:~$ date
Mon 31 Aug 2020 03:03:41 AM MSK
```

#### Список доступных часовых поясов

```markdown
user@computer:~$ timedatectl list-timezones
Africa/Abidjan
Africa/Accra
...
Europe/Astrakhan
Europe/Kaliningrad
Europe/Kiev
Europe/Kirov
Europe/Moscow
Europe/Samara
Europe/Saratov
Europe/Simferopol
Europe/Ulyanovsk
Europe/Uzhgorod
Europe/Volgograd
...
Pacific/Wake
Pacific/Wallis
UTC
```

#### История команд

```markdown
history <NUMBER>
```

где:

- `<NUMBER>` - количество команд

Результатом команды `history` будет вывод всей истории команд:

```markdown
    1  service apache2 status
    2  service apache2 restart
    3  ls -alh
    4  php -v
    5  php -m
...
   16  dpkg --list | grep php7.4
   17  apt-get install php7.4-zip
   18  dpkg --list | grep php7.4
   19  exit
   20  history
```

Результатом команды `history 5` будет вывод последних 5 команд:

```markdown
   17  apt-get install php7.4-zip
   18  dpkg --list | grep php7.4
   19  exit
   20  history
   21  history 5
```

#### Очистка истории команд

```markdown
history -c
```

## <a name="source"></a> Источник [&uarr;](#content "Содержание")

- [История команд Linux (losst.ru)](https://losst.ru/istoriya-komand-linux)
- [Выключение Linux из командной строки (losst.ru)](https://losst.ru/vyklyuchenie-linux-iz-komandnoj-stroki)