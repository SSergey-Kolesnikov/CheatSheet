[&larr;](../readme.md "Шпаргалка") SSH команды
----------------------------------------------

## <a name="content"></a> Содержание:

- [Apache](apache.md "Apache")
- [Git](git.md "Git")
- [Midnight Commander](midnight-commander.md "Midnight Commander")
- [MySQL](mysql.md "MySQL")
- [PHP](php.md "PHP")
- [Архиваторы](archivers.md "Архиваторы")
- [Мониторинг работы системы, нагрузки сервера, сети и т.п.](monitoring-system-operation-server-load-network-etc.md "Мониторинг работы системы, нагрузки сервера, сети и т.п.")
- [Файловая система](file-system.md "Файловая система")
- [Прочие команды](#other-commands "Прочие команды")
- [Источник](#source)

## <a name="other-commands"></a> Прочие команды [&uarr;](#content "Содержание")

#### Название ОС

```markdown
uname -a
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