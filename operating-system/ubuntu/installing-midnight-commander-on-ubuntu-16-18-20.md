[&larr;](readme.md "Ubuntu") Установка Midnight Commander на Ubuntu 16/18/20
----------------------------------------------------------------------------

Midnight Commander - один из файловых менеджеров с текстовым интерфейсом типа Norton Commander для UNIX-подобных операционных систем.

## <a name="content"></a> Содержание:

- [Обновление системы](#system-update)
- [Установка](#installation)
- [Источники](#sources)

### <a name="system-update"></a> Обновление системы [&uarr;](#content "Содержание")

Обновляем список пакетов:

```markdown
user@computer:~$ apt update
```

Просматриваем список пакетов, которые требуют обновления:

```markdown
user@computer:~$ apt list --upgradable
```

Обновляем пакеты, установленные в системе:

```markdown
user@computer:~$ apt upgrade
```

### <a name="installation"></a> Установка [&uarr;](#content "Содержание")

Устанавливаем Midnight Commander:

```markdown
user@computer:~$ apt install mc
```

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [Midnight Commander (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Midnight_Commander)