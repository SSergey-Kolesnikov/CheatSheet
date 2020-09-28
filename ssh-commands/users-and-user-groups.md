[&larr;](readme.md "SSH команды") Пользователи и группы пользователей
---------------------------------------------------------------------

#### Список пользователей:

```markdown
user@computer:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
...
```

#### Список групп пользователей:

```markdown
user@computer:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
...
```

#### Список групп текущего пользователя:

```markdown
user@computer:~$ id -Gn
adm cdrom sudo
```

или

```markdown
user@computer:~$ groups
adm cdrom sudo
```

#### Список групп определенного пользователя:

```markdown
user@computer:~$ id -Gn <USER>
<USER> : adm cdrom sudo
```

или

```markdown
user@computer:~$ groups <USER>
<USER> : adm cdrom sudo
```

где:

- `<USER>` - логин пользователя;

#### Создание группы пользователей:

```markdown
user@computer:~$ groupadd <GROUP>
```

где:

- `<GROUP>` - наименование группы пользователей;

#### Переименование группы пользователей:

```markdown
user@computer:~$ groupmod -n <NEW_GROUP> <OLD_GROUP> 
```

где:

- `<NEW_GROUP>` - новое наименование группы пользователей;
- `<OLD_GROUP>` - переименовываемая группа пользователей;

## Источники

- [Пользователи и группы (help.ubuntu.ru)](https://help.ubuntu.ru/wiki/%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D0%B8_%D0%B8_%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D1%8B)
- [Список групп пользователя Linux (losst.ru)](https://losst.ru/spisok-grupp-polzovatelya-linux)
- [Группы пользователей Linux (losst.ru)](https://losst.ru/gruppy-polzovatelej-linux)
- [Как создать группу Linux (losst.ru)](https://losst.ru/kak-sozdat-gruppu-linux)
- [Как создать пользователя Linux (losst.ru)](https://losst.ru/kak-sozdat-polzovatelya-linux)
- [Как посмотреть пользователей Ubuntu (losst.ru)](https://losst.ru/kak-posmotret-spisok-polzovatelej-v-ubuntu)
- [Изменить имя пользователя/группы в любом Linux (itsecforu.ru)](https://itsecforu.ru/2017/06/14/%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B8%D1%82%D1%8C-%D0%B8%D0%BC%D1%8F-%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F%D0%B3%D1%80%D1%83%D0%BF%D0%BF%D1%8B-%D0%B2-%D0%BB%D1%8E/)