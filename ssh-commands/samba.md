[&larr;](readme.md "SSH команды") Samba
---------------------------------------

#### Статус Samba

```markdown
user@computer:~$ systemctl status smbd
```

#### Список пользователей Samba:

```markdown
user@computer:~$ pdbedit -L
<USER>:<ID>:<NAME>
...
```

где:

- `<USER>` - логин пользователя;
- `<ID>` - id пользователя;
- `<NAME>` - имя пользователя;

#### Список пользователей Samba с расширенной информацией:

```markdown
user@computer:~$ pdbedit -L -v
---------------
Unix username:        <USER>
NT username:
Account Flags:        [U          ]
User SID:             S-1-5-21-2626010435-3412487033-741123865-<USER_ID>
Forcing Primary Group to 'Domain Users' for <USER>
Primary Group SID:    S-1-5-21-2626010435-3412487033-741123865-<GROUP_ID>
Full Name:            <NAME>
Home Directory:       \\<PATH_HOME>
HomeDir Drive:
Logon Script:
Profile Path:         \\<PATH_PROFILE>
Domain:               <DOMAIN>
Account desc:
Workstations:
Munged dial:
Logon time:           0
Logoff time:          Wed, 06 Feb 2036 18:06:39 MSK
Kickoff time:         Wed, 06 Feb 2036 18:06:39 MSK
Password last set:    Mon, 31 Aug 2020 23:56:52 MSK
Password can change:  Mon, 31 Aug 2020 23:56:52 MSK
Password must change: never
Last bad password   : 0
Bad password count  : 0
Logon hours         : FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF

```

где:

- `<USER>` - логин пользователя;
- `<USER_ID>` - id пользователя;
- `<GROUP_ID>` - id группы пользователей;
- `<NAME>` - имя пользователя;
- `<PATH_HOME>` - путь до домашней папки;
- `<PATH_PROFILE>` - путь до профиля;
- `<DOMAIN>` - домен;

## Источники

- [Вывести список пользователей Samba (itfound.ru)](http://itfound.ru/72-samba-list-users.html)