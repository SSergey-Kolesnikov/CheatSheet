[&larr;](readme.md "Ubuntu") Установка Webmin на Ubuntu Server 20
-----------------------------------------------------------------

Webmin — это программный комплекс, позволяющий администрировать операционную систему через веб-интерфейс, в большинстве случаев, позволяя обойтись без использования командной строки и запоминания системных команд и их параметров. Используя любой браузер, администратор сервера может создавать новые учётные записи пользователей, почтовые ящики, изменять настройки служб и сервисов, например: веб-сервера Apache, DNS. Однако, в некоторых случаях необходимо знание операционной системы и редактирование конфигурационных файлов вручную. Кроме того, не все возможности операционной системы и не все программы можно конфигурировать через интерфейс Webmin, например nginx пока не входит в базовый набор.

Webmin состоит из простого веб-сервера и большого количества скриптов (>500), которые собственно и осуществляют связь между командами администратора через веб-интерфейс и их исполнением на уровне операционной системы и прикладных программ. Webmin написан полностью на языке Perl и не использует никаких дополнительных нестандартных модулей. Простота, лёгкость и быстрота выполнения команд — одно из самых больших преимуществ данной панели управления.

Другое важное преимущество — возможность исправлять конфигурационные файлы вручную, так как Webmin не «портит» конфигурационные файлы, в отличие от некоторых других панелей управления, и следует, как правило, политикам дистрибутивов по конфигурированию программ.

## <a name="content"></a> Содержание:

- [Установка](#installation)
- [Источники](#sources)

## <a name="installation"></a> Установка

Добавляем официальный репозиторий Webmin в источники приложений, для этого открываем файл `/etc/apt/sources.list` на редактирование:

```markdown
user@computer:~$ sudo nano /etc/apt/sources.list
```

В конец файла добавляем строки:

```markdown
deb http://download.webmin.com/download/repository sarge contrib
deb http://webmin.mirror.somersettechsolutions.co.uk/repository sarge contrib
```

Скачиваем GPG-ключ репозитория:

```markdown
user@computer:~$ sudo wget http://www.webmin.com/jcameron-key.asc
--0000-00-00 00:00:00--  http://www.webmin.com/jcameron-key.asc
Resolving www.webmin.com (www.webmin.com)... 216.105.38.10
Connecting to www.webmin.com (www.webmin.com)|216.105.38.10|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1320 (1.3K) [text/plain]
Saving to: ‘jcameron-key.asc’

jcameron-key.asc                            100%[=========================================================================================>]   1.29K  --.-KB/s    in 0s

0000-00-00 00:00:00 (46.9 MB/s) - ‘jcameron-key.asc’ saved [1320/1320]
```

Добавляем GPG-ключ репозитория:

```markdown
user@computer:~$ sudo apt-key add jcameron-key.asc
OK
```

Обновляем списки пакетов:

```markdown
user@computer:~$ sudo apt update
Hit:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [111 kB]
Get:3 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [98.3 kB]
Get:4 http://ru.archive.ubuntu.com/ubuntu focal-security InRelease [107 kB]
Ign:5 http://webmin.mirror.somersettechsolutions.co.uk/repository sarge InRelease
Get:6 http://webmin.mirror.somersettechsolutions.co.uk/repository sarge Release [16.9 kB]
Get:7 http://webmin.mirror.somersettechsolutions.co.uk/repository sarge Release.gpg [173 B]
Ign:8 http://download.webmin.com/download/repository sarge InRelease
Get:9 http://webmin.mirror.somersettechsolutions.co.uk/repository sarge/contrib amd64 Packages [1,393 B]
Get:10 http://download.webmin.com/download/repository sarge Release [16.9 kB]
Get:11 http://download.webmin.com/download/repository sarge Release.gpg [173 B]
Get:12 http://download.webmin.com/download/repository sarge/contrib amd64 Packages [1,393 B]
Fetched 354 kB in 3s (127 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
All packages are up to date.
```

Устанавливаем Webmin:

```markdown
user@computer:~$ sudo apt install webmin
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  apt-show-versions libapt-pkg-perl libauthen-pam-perl libio-pty-perl libnet-ssleay-perl perl-openssl-defaults
The following NEW packages will be installed:
  apt-show-versions libapt-pkg-perl libauthen-pam-perl libio-pty-perl libnet-ssleay-perl perl-openssl-defaults webmin
0 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.
Need to get 29.7 MB of archives.
After this operation, 310 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 perl-openssl-defaults amd64 4 [7,192 B]
Get:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libnet-ssleay-perl amd64 1.88-2ubuntu1 [291 kB]
Get:3 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libauthen-pam-perl amd64 0.16-3build7 [24.3 kB]
Get:4 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libio-pty-perl amd64 1:1.12-1 [32.4 kB]
Get:5 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libapt-pkg-perl amd64 0.1.36build3 [68.5 kB]
Get:6 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 apt-show-versions all 0.22.11 [28.8 kB]
Get:7 http://download.webmin.com/download/repository sarge/contrib amd64 webmin all 1.955 [29.3 MB]
Fetched 29.7 MB in 7s (3,992 kB/s)
Selecting previously unselected package perl-openssl-defaults:amd64.
(Reading database ... 71302 files and directories currently installed.)
Preparing to unpack .../0-perl-openssl-defaults_4_amd64.deb ...
Unpacking perl-openssl-defaults:amd64 (4) ...
Selecting previously unselected package libnet-ssleay-perl.
Preparing to unpack .../1-libnet-ssleay-perl_1.88-2ubuntu1_amd64.deb ...
Unpacking libnet-ssleay-perl (1.88-2ubuntu1) ...
Selecting previously unselected package libauthen-pam-perl.
Preparing to unpack .../2-libauthen-pam-perl_0.16-3build7_amd64.deb ...
Unpacking libauthen-pam-perl (0.16-3build7) ...
Selecting previously unselected package libio-pty-perl.
Preparing to unpack .../3-libio-pty-perl_1%3a1.12-1_amd64.deb ...
Unpacking libio-pty-perl (1:1.12-1) ...
Selecting previously unselected package libapt-pkg-perl.
Preparing to unpack .../4-libapt-pkg-perl_0.1.36build3_amd64.deb ...
Unpacking libapt-pkg-perl (0.1.36build3) ...
Selecting previously unselected package apt-show-versions.
Preparing to unpack .../5-apt-show-versions_0.22.11_all.deb ...
Unpacking apt-show-versions (0.22.11) ...
Selecting previously unselected package webmin.
Preparing to unpack .../6-webmin_1.955_all.deb ...
Unpacking webmin (1.955) ...
Setting up libapt-pkg-perl (0.1.36build3) ...
Setting up libio-pty-perl (1:1.12-1) ...
Setting up apt-show-versions (0.22.11) ...
** initializing cache. This may take a while **
Setting up perl-openssl-defaults:amd64 (4) ...
Setting up libauthen-pam-perl (0.16-3build7) ...
Setting up libnet-ssleay-perl (1.88-2ubuntu1) ...
Setting up webmin (1.955) ...
/var/lib/dpkg/info/webmin.postinst: 4: cannot create /etc/webmin/stop: Directory nonexistent
Webmin install complete. You can now login to https://<IP>:10000/
as root with your root password, or as any user who can use sudo
to run commands as root.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.2) ...
```

В брандмауэре открываем порт 10000 для Webmin:

```markdown
user@computer:~$ sudo ufw allow 10000
Rule added
Rule added (v6)
```

На этом Webmin установлен и доступен по ссылке в браузере `https://<IP>:10000/`, где `IP` - это IP компьютера в локальной сети.

## <a name="sources"></a> Источники

- [Webmin (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Webmin)
- [Установка Webmin на Ubuntu Server 20.04 (losst.ru)](https://losst.ru/ustanovka-webmin-na-ubuntu-server-16-04)