[&larr;](readme.md "Ubuntu") Файл `sources.list` для Ubuntu 16.04
-----------------------------------------------------------------

<a name="content"></a>
## Содержание:

- [Расположение файла](#file-location)
- [Содержимое файла](#file-contents)
- [Источники](#sources)

<a name="file-location"></a>
## Расположение файла

Файл `sources.list` для Ubuntu 16.04 располагается в папке `/etc/aptsources.list`.

<a name="file-contents"></a>
## Содержимое файла

```
## SOURCES LIST FOR UBUNTU 16.04 LTS XENIAL XERUS
## ALSO FOR XUBUNTU 16.04, LUBUNTU 16.04
## AND KUBUNTU 16.04
## From: http://sites.google.com/site/easylinuxtipsproject
## This list is for the Main server; you might want to select a
## faster mirror server closer to you, with Software & Updates.
## Only fit for 16.04 LTS Xenial Xerus!
#
## SOURCES FOR ORDINARY UPDATES AND SOFTWARE:
deb http://archive.ubuntu.com/ubuntu xenial main
deb http://archive.ubuntu.com/ubuntu xenial-updates main
deb http://archive.ubuntu.com/ubuntu xenial restricted
deb http://archive.ubuntu.com/ubuntu xenial-updates restricted
deb http://archive.ubuntu.com/ubuntu xenial universe
deb http://archive.ubuntu.com/ubuntu xenial-updates universe
deb http://archive.ubuntu.com/ubuntu xenial multiverse
deb http://archive.ubuntu.com/ubuntu xenial-updates multiverse
#
## SOURCES FOR SECURITY UPDATES:
deb http://archive.ubuntu.com/ubuntu xenial-security main
deb http://archive.ubuntu.com/ubuntu xenial-security restricted
deb http://archive.ubuntu.com/ubuntu xenial-security universe
deb http://archive.ubuntu.com/ubuntu xenial-security multiverse
#
## BACKPORTS SOURCES (WITH LOWERED PRIORITY):
deb http://archive.ubuntu.com/ubuntu xenial-backports main
deb http://archive.ubuntu.com/ubuntu xenial-backports restricted
deb http://archive.ubuntu.com/ubuntu xenial-backports universe
deb http://archive.ubuntu.com/ubuntu xenial-backports multiverse
#
## PARTNER SOURCE (FOR SOFTWARE FROM
## PARTNERS OF CANONICAL):
deb http://archive.canonical.com/ubuntu xenial partner
```

<a name="sources"></a>
## Источники

- [Ubuntu 16.04 sources.list file. Might be useful. (securitronlinux.com)](https://securitronlinux.com/debian-testing/ubuntu-16-04-sources-list-file-might-be-useful/)