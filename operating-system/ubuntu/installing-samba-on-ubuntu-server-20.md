[&larr;](readme.md "Ubuntu") Установка Samba на Ubuntu Server 20
-----------------------------------------------------------------

Samba — пакет программ, которые позволяют обращаться к сетевым дискам и принтерам на различных операционных системах по протоколу SMB/CIFS. Имеет клиентскую и серверную части.

<a name="content"></a>
## Содержание:

- [Установка](#installation)
- [Базования настройка](#base-setting)
- [Пользователи](#users)
- [Создание папок](#create-folders)
- [Подведение итогов](#summarizing)
- [Источники](#sources)

<a name="installation"></a>
## Установка

Обновляем список пакетов:

```markdown
user@computer:~$ sudo apt update
Hit:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease
Hit:4 http://ru.archive.ubuntu.com/ubuntu focal-security InRelease
Reading package lists... Done
Building dependency tree
Reading state information... Done
All packages are up to date.
```

Устанавливаем Samba:

```markdown
user@computer:~$ sudo apt install samba
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  attr ibverbs-providers libavahi-client3 libavahi-common-data libavahi-common3 libboost-iostreams1.71.0 libboost-thread1.71.0 libcephfs2 libcups2 libibverbs1 libjansson4 libldb2 libnl-route-3-200
  librados2 librdmacm1 libtalloc2 libtevent0 libwbclient0 python3-crypto python3-dnspython python3-gpg python3-ldb python3-markdown python3-packaging python3-pygments python3-pyparsing python3-samba
  python3-talloc python3-tdb samba-common samba-common-bin samba-dsdb-modules samba-libs samba-vfs-modules tdb-tools
Suggested packages:
  cups-common python-markdown-doc python-pygments-doc ttf-bitstream-vera python-pyparsing-doc bind9 bind9utils ctdb ldb-tools smbldap-tools winbind heimdal-clients
The following NEW packages will be installed:
  attr ibverbs-providers libavahi-client3 libavahi-common-data libavahi-common3 libboost-iostreams1.71.0 libboost-thread1.71.0 libcephfs2 libcups2 libibverbs1 libjansson4 libldb2 libnl-route-3-200
  librados2 librdmacm1 libtalloc2 libtevent0 libwbclient0 python3-crypto python3-dnspython python3-gpg python3-ldb python3-markdown python3-packaging python3-pygments python3-pyparsing python3-samba
  python3-talloc python3-tdb samba samba-common samba-common-bin samba-dsdb-modules samba-libs samba-vfs-modules tdb-tools
0 upgraded, 36 newly installed, 0 to remove and 0 not upgraded.
Need to get 16.7 MB of archives.
After this operation, 98.4 MB of additional disk space will be used.
Do you want to continue? [Y/n] y

...

Checking smb.conf with testparm
Load smb config files from /etc/samba/smb.conf
Loaded services file OK.
Server role: ROLE_STANDALONE

Done
Setting up samba (2:4.11.6+dfsg-0ubuntu1.4) ...
Adding group `sambashare' (GID 119) ...
Done.
Samba is not being run as an AD Domain Controller: Masking samba-ad-dc.service
Please ignore the following error about deb-systemd-helper not finding those services.
(samba-ad-dc.service masked)
Created symlink /etc/systemd/system/multi-user.target.wants/nmbd.service → /lib/systemd/system/nmbd.service.
Failed to preset unit: Unit file /etc/systemd/system/samba-ad-dc.service is masked.
/usr/bin/deb-systemd-helper: error: systemctl preset failed on samba-ad-dc.service: No such file or directory
Created symlink /etc/systemd/system/multi-user.target.wants/smbd.service → /lib/systemd/system/smbd.service.
samba-ad-dc.service is a disabled or a static unit, not starting it.
Processing triggers for ufw (0.36-6) ...
Rules updated for profile 'OpenSSH'
Skipped reloading firewall
Processing triggers for systemd (245.4-4ubuntu3.2) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9) ...
```

Проверяем, запущены ли службы Samba, которые обеспечивают доступ к файлам и принтерам:

```markdown
user@computer:~$ sudo systemctl status smbd
● smbd.service - Samba SMB Daemon
     Loaded: loaded (/lib/systemd/system/smbd.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-08-27 19:02:32 MSK; 10min ago
       Docs: man:smbd(8)
             man:samba(7)
             man:smb.conf(5)
   Main PID: 3739 (smbd)
     Status: "smbd: ready to serve connections..."
      Tasks: 4 (limit: 3488)
     Memory: 8.3M
     CGroup: /system.slice/smbd.service
             ├─3739 /usr/sbin/smbd --foreground --no-process-group
             ├─3741 /usr/sbin/smbd --foreground --no-process-group
             ├─3742 /usr/sbin/smbd --foreground --no-process-group
             └─3743 /usr/sbin/smbd --foreground --no-process-group

Aug 27 19:02:31 computer systemd[1]: Starting Samba SMB Daemon...
Aug 27 19:02:31 computer update-apparmor-samba-profile[3733]: grep: /etc/apparmor.d/samba/smbd-shares: No such file or directory
Aug 27 19:02:31 computer update-apparmor-samba-profile[3736]: diff: /etc/apparmor.d/samba/smbd-shares: No such file or directory
Aug 27 19:02:32 computer systemd[1]: Started Samba SMB Daemon.
```

По умолчанию службы Samba включены, поэтому они будут запускаться вместе с ОС без дополнительных действий.

<a name="base-setting"></a>
## Базования настройка

> Настройка Samba - это самый геморройный геморрой в мире геморроя!

Делаем резервную копию файла настроек Samba:

```markdown
user@computer:~$ sudo cp /etc/samba/smb.conf{,.backup}
```

Теперь, на всякий случай, есть файл (`/etc/samba/smb.conf.backup`) с дефолтными настройками Samba и всегда можно откатиться к нему.

Открываем файл с настройками Samba на редактирование с правами рута:

```markdown
user@computer:~$ sudo nano /etc/samba/smb.conf
```

И прописываем настройки Samba:

```markdown
[global]

workgroup = WORKGROUP
netbios name = SERVER
server string = %h (Samba, Ubuntu)
server role = standalone server
os level = 65

log file = /var/log/samba/log.%m
max log size = 1000
log level = 3
debug timestamp = yes

security = user
map to guest = bad user
usershare allow guests = yes

#======================= Share Definitions =======================

[Shared]
comment = Shared files
path = /mnt/shared
guest ok = yes
browseable = yes
writeable = no
create mask = 0770
directory mask = 2770
force create mode = 0770
force directory mode = 2770
write list = @group
```

где:

- `workgroup` - рабочая группа, по умолчанию WORKGROUP;
- `netbios name` - имя компьютера, которое будет отображаться в сетевом окружении;
- `server string` - описание компьютера;
    - `%h` - макрос, который будет заменен именем компьютера;
- `server role` - режим работы сервера;
- `os level` - приоритет данного сервера среди других компьютеров рабочей группы. Определяет, кто именно будет главной машиной, отвечающей за отображение ресурсов сети. Для сравнения, у Win9X os level = 34, а у NT4 os level = 64;
- `log file` - путь до логов;
- `max log size` - ограничение размера отдельных файлов с логами (Kb);
- `log level` - уровень детализации логов;
- `debug timestamp` - добавление временных меток в логи;
- `security` - уровень безопасности сервера;
    - `user` - авторизация по паре логин/пароль;
- `map to guest` - определение способа обработки запросов;
    - `bad user` - запросы с неправильным паролем будут отклонены, даже если такое имя пользователя существует;
- `usershare allow guests` - позволяет не аутентифицированным пользователям получить доступ к общим ресурсам пользователей;

В блоке `Share Definitions` прописываем настройки папок:

- `comment` - комментарий в свободной форме;
- `path` - путь к папке;
- `guest ok` - возможность доступа к каталогу без пароля (гостевой);
- `browseable` - показывать ли каталог на сервере среди прочих;
- `writeable` - позволяет ли пользователям выполнять действия над файлами внутри каталога — переименование, добавление, удаление, перемещение в подкаталог и копирование;
- `create mask` - маска прав для создаваемых файлов;
- `directory mask` - маска прав для создаваемых папок;
- `force create mode` - маска прав, которые будут всегда устанавливаться на файле;
- `force directory mode` - маска прав, которые будут всегда устанавливаться на папках;
- `write list` - список пользователей или групп пользователей, имеющих доступ на чтение/запись;

Проверяем утилитой testparm (входит в пакет Samba) правильность настроек:

```markdown
user@computer:~$ testparm -s
Load smb config files from /etc/samba/smb.conf
Loaded services file OK.
...
```

В брандмауэре разрешаем Samba:

```markdown
user@computer:~$ sudo ufw allow Samba
Rule added
Rule added (v6)
```

<a name="users"></a>
## Пользователи

Создаем пользователя Samba и устанавливаем пароль:

```markdown
user@computer:~$ sudo smbpasswd -a user
New SMB password:
Retype new SMB password:
Added user user.
```

Включаем пользователя Samba:

```markdown
user@computer:~$ sudo smbpasswd -e user
Enabled user user.
```

Создаем группу пользователей под дополнительного пользователя:

```markdown
user@computer:~$ groupadd user2
```

Создаем дополнительного пользователя:

```markdown
user@computer:~$ sudo useradd -M -d /mnt/user2 -s /usr/sbin/nologin -g user2 user2
```

где:

- `-M` — домашний каталог пользователя не создается, каталог будет создан вручную;
- `-d /mnt/user2` — домашний каталог пользователя;
- `-s /usr/sbin/nologin` — отключаем доступ к оболочке для пользователя;
- `-g user2` — добавляем пользователя в групп user2;

Указываем пароль для созданного пользователя:

```markdown
user@computer:~$ sudo passwd user2
```

Создаем дополнительного пользователя Samba и устанавливаем пароль:

```markdown
user@computer:~$ sudo smbpasswd -a user2
New SMB password:
Retype new SMB password:
Added user user2.
```

Включаем дополнительного пользователя Samba:

```markdown
user@computer:~$ sudo smbpasswd -e user2
Enabled user user2.
```

Создаем группу пользователей для объединения текущего пользователя и дополнительного пользователя:

```markdown
user@computer:~$ groupadd group
```

Добавляем текущего пользователя в общую группу пользователей.

```markdown
user@computer:~$ sudo usermod -a -G group user
```

Добавляем дополнительного пользователя в общую группу пользователей.

```markdown
user@computer:~$ sudo usermod -a -G group user2
```

Перезапускаем сервисы Samba:

```markdown
user@computer:~$ sudo systemctl restart smbd
```

<a name="create-folders"></a>
## Создание папок

Создаем папки, описанные в файле настроек Samba `/etc/samba/smb.conf` в блоке `Share Definitions`:

```markdown
user@computer:~$ sudo mkdir /mnt/shared
```

Меняем владельца папки на `user` и группу пользователей `group`:

```markdown
user@computer:~$ sudo chown user:group /mnt/shared
```

Меняем права на созданную папку:

```markdown
user@computer:~$ sudo chmod -R 2770 /mnt/shared
```

<a name="summarizing"></a>
## Подведение итогов

В итоге у нас в сетевом окружении появится сервер с папками:

- `Shared` - общая папка с доступом на чтение для всех пользователей и для записи только для пользователей, входящих в группу `group`;

<a name="sources"></a>
## Источники

- [Samba (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Samba)
- [Samba (help.ubuntu.ru)](https://help.ubuntu.ru/wiki/samba)
- [Все о Samba (smb-conf.ru)](https://smb-conf.ru/)
- [Настройка Samba (adminunix.ru)](https://adminunix.ru/nastrojka-samba/)
- [How to configure Samba Server share on Ubuntu 20.04 Focal Fossa Linux (linuxconfig.org)](https://linuxconfig.org/how-to-configure-samba-server-share-on-ubuntu-20-04-focal-fossa-linux)
- [Install Samba on Ubuntu 20.04 | 18.04 (websiteforstudents.com)](https://websiteforstudents.com/install-samba-on-ubuntu-20-04-18-04/)
- [Настройка файлового сервера Samba на платформе Debian / Ubuntu (interface31.ru)](https://interface31.ru/tech_it/2019/06/nastroyka-faylovogo-servera-samba-na-platforme-debian-ubuntu.html)
- [Samba. Установка и простая настройка. (linuxrussia.com)](https://linuxrussia.com/samba-basic-setup.html)
- [Настройка Samba (serverspace.by)](https://serverspace.by/support/help/nastroika-samba/)
- [Установка SAMBA на Ubuntu Server (obu4alka.ru)](https://obu4alka.ru/ustanovka-samba-na-ubuntu-server.html)
- [Настройка samba в Ubuntu 18.04 (losst.ru)](https://losst.ru/nastrojka-samba-v-ubuntu-15-10)
- [Samba (linux.yaroslavl.ru)](http://linux.yaroslavl.ru/docs/altlinux/master20_u/ch09s04.html)
- [Конфигурация Samba сервера. (linux.yaroslavl.ru)](http://linux.yaroslavl.ru/docs/serv/samba/samba_conf.html)
- [Детальные логи в Samba (ixnfo.com)](https://ixnfo.com/detalnye-logi-samba.html)
- [Samba. Управление доступом. (linuxrussia.com)](https://linuxrussia.com/samba-access-control.html)
- [Фундаментальные основы Linux. Часть VIII. Механизмы безопасной работы с файлами (rus-linux.net)](http://rus-linux.net/MyLDP/BOOKS/Linux_Foundations/31/ch31.html)
