[&larr;](readme.md "SSH команды") Файловая система
--------------------------------------------------

<a name="content"></a>
## Содержание:

- [Копирование](#copying)
    - [Копирование файлов](#copying-files)
    - [Копирование папок](#copying-folders)
- [Удаление](#deleting)
    - [Удаление файлов](#deleting-files)
    - [Удаление папок](#deleting-folders)
- [Права доступа](#access-rights)
- [Анализ дискового пространства](#disk-space-aanalysis)
- [Прочее](#other)
- [Источники](#sources)

<a name="copying"></a>
## Копирование

<a name="copying-files"></a>
### Копирование файлов

#### Копирование файла с текущего сервера на удаленный сервер

```markdown
user@computer:~$ scp <PATH_FROM> <USER>@<IP>:<PATH_TO>
```

где:

- `<PATH_FROM>` - путь до копируемого файла (если файл надо скопировать из текущей папки, то достаточно указать имя файла);
- `<USER>` - пользователь на сервере, куда копируется файл;
- `<IP>` - IP-адрес сервера, куда копируется файл;
- `<PATH_TO>` - путь до папки на сервере, куда копируется файл;

Пример:

```markdown
user@computer:~$ scp /folder_from_1/folder_from_2/file.txt root@127.0.0.1:/folder_to_1/folder_to_2/
root@185.60.135.238's password:
file.txt                                                              100% 5504MB  11.1MB/s   08:17
```

<a name="copying-folders"></a>
### Копирование папок

#### Копирование папки с текущего сервера на удаленный сервер

```markdown
user@computer:~$ scp -r <PATH_FROM> <USER>@<IP>:<PATH_TO>
```

где:

- `r` - ключ, указывающий на рекурсивное копирование папок (включая подкаталоги);
- `<PATH_FROM>` - путь до копируемой папки;
- `<USER>` - пользователь на сервере, куда копируется папка;
- `<IP>` - IP-адрес сервера, куда копируется папка;
- `<PATH_TO>` - путь до папки на сервере, куда копируется папка;

Пример:

```markdown
user@computer:~$ scp -r /folder_from_1/folder_from_2/ root@127.0.0.1:/folder_to_1/folder_to_2/
```

В данном примере в папке `folder_to_2` будет создана папка `folder_from_2` и в нее будет скопировано все содержимое.

<a name="deleting"></a>
## Удаление

<a name="deleting-files"></a>
### Удаление файлов

#### Удаление файла

```markdown
user@computer:~$ rm -f <PATH_TO_FILE>/<FILE>
```

где:
 
- `f` - разрешение на удаление файла без запроса;
- `<PATH_TO_FILE>` - путь до папки с файлом;
- `<FILE>` - наименование файла с расширением;

<a name="deleting-folders"></a>
### Удаление папок

#### Удаление папки

```markdown
rm -Rfv <PATH_TO_FOLDER>
```

где:
 
- `R` - рекурсивное удаление всех подпапок и файлов в них;
- `f` - разрешение на удаление подпапок и файлов без запроса;
- `v` - показ удаляемых имен папок и файлов;
- `<PATH_TO_FOLDER>` - путь до папки;

<a name="access-rights"></a>
## Права доступа

#### Меняем права на папку (рекурсивно)

```markdown
chmod -R <ACCESS_RIGHTS> <PATH_TO_FOLDER>
```

где:
 
- `<ACCESS_RIGHTS>` - права доступа;
- `<PATH_TO_FOLDER>` - путь до папки;

#### Меняем владельца папок и файлов (рекурсивно)

```markdown
chown -R <USER>:<GROUP> <PATH_TO_FOLDER>
```

где:
 
- `<USER>` - логин пользователя;
- `<GROUP>` - группа пользователей;
- `<PATH_TO_FOLDER>` - путь до папки;

#### Меняем владельца всех папок и файлов (рекурсивно) в текущей папке

```markdown
chown -R <USER>:<GROUP> ./*
```

где:
 
- `<USER>` - логин пользователя;
- `<GROUP>` - группа пользователей;

<a name="disk-space-aanalysis"></a>
## Анализ дискового пространства

#### Анализ дискового пространства (всего/занято/свободно)

```markdown
df -h /
```

#### Смотрим объем указанной папки

```markdown
du -sh <PATH_TO_FOLDER>
```

где:

- `<PATH_TO_FOLDER>` - путь до папки;

#### Смотрим объем всех папок в текущей папке

```markdown
du -sh *
```

<a name="other"></a>
## Прочее

#### Переход в домашнюю папку

```markdown
cd ~
```

#### Смотрим, что лежит папке

```markdown
ls -alh <PATH_TO_FOLDER>
```

где:

- `a` - говорит что нужно показать даже скрытые файлы;
- `l` - позволяет показать полную информацию о файле(права, размер, пользователя, дату);
- `h` - делает вывод более читабельным;
- `<PATH_TO_FOLDER>` - путь до папки;

#### Список подключенных дисков

```markdown
user@computer:~$ ls -l /dev/ | grep sd
brw-rw---- 1 root disk      8,   0 Aug 31 03:51 sda
brw-rw---- 1 root disk      8,   1 Aug 31 03:51 sda1
brw-rw---- 1 root disk      8,  16 Aug 31 03:51 sdb
brw-rw---- 1 root disk      8,  17 Aug 31 03:51 sdb1
brw-rw---- 1 root disk      8,  18 Aug 31 03:51 sdb2
brw-rw---- 1 root disk      8,  19 Aug 31 03:51 sdb3
brw-rw---- 1 root disk      8,  20 Aug 31 03:51 sdb4
```

```markdown
user@computer:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            1.5G     0  1.5G   0% /dev
tmpfs           300M  2.6M  297M   1% /run
/dev/sdb2        40G  5.8G   32G  16% /
tmpfs           1.5G     0  1.5G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           1.5G     0  1.5G   0% /sys/fs/cgroup
/dev/sdb3        98G   61M   93G   1% /home
/dev/sda1        73G  1.6G   68G   3% /mnt/disk1
/dev/loop1       55M   55M     0 100% /snap/core18/1880
/dev/loop0       56M   56M     0 100% /snap/core18/1885
/dev/loop2       72M   72M     0 100% /snap/lxd/16099
/dev/loop5       30M   30M     0 100% /snap/snapd/8790
/dev/loop4       30M   30M     0 100% /snap/snapd/8542
/dev/loop3       71M   71M     0 100% /snap/lxd/16922
tmpfs           300M     0  300M   0% /run/user/1000
```

```markdown
user@computer:~$ 
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0    7:0    0  55.3M  1 loop /snap/core18/1885
loop1    7:1    0    55M  1 loop /snap/core18/1880
loop2    7:2    0  71.3M  1 loop /snap/lxd/16099
loop3    7:3    0  70.6M  1 loop /snap/lxd/16922
loop4    7:4    0  29.9M  1 loop /snap/snapd/8542
loop5    7:5    0  29.9M  1 loop /snap/snapd/8790
sda      8:0    0  74.6G  0 disk
└─sda1   8:1    0  74.6G  0 part /mnt/disk1
sdb      8:16   0 149.1G  0 disk
├─sdb1   8:17   0     1M  0 part
├─sdb2   8:18   0    40G  0 part /
├─sdb3   8:19   0   100G  0 part /home
└─sdb4   8:20   0     9G  0 part [SWAP]
```

```markdown
user@computer:~$ fdisk -l
Disk /dev/loop0: 55.33 MiB, 58007552 bytes, 113296 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop1: 54.98 MiB, 57626624 bytes, 112552 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop2: 71.28 MiB, 74735616 bytes, 145968 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop3: 70.58 MiB, 73990144 bytes, 144512 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop4: 29.9 MiB, 31334400 bytes, 61200 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/loop5: 29.91 MiB, 31342592 bytes, 61216 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sda: 74.58 GiB, 80060424192 bytes, 156368016 sectors
Disk model: SAMSUNG SP0802N
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: D57F046B-3DFB-45DA-8BB4-61A75597789E

Device     Start       End   Sectors  Size Type
/dev/sda1   2048 156364799 156362752 74.6G Linux filesystem


Disk /dev/sdb: 149.5 GiB, 160041885696 bytes, 312581808 sectors
Disk model: ST3160827AS
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 7B755024-F020-4502-9880-52AF9339C99B

Device         Start       End   Sectors  Size Type
/dev/sdb1       2048      4095      2048    1M BIOS boot
/dev/sdb2       4096  83890175  83886080   40G Linux filesystem
/dev/sdb3   83890176 293605375 209715200  100G Linux filesystem
/dev/sdb4  293605376 312578047  18972672    9G Linux swap
```

<a name="sources"></a>
## Источники

- [Как удалить каталог Linux (losst.ru)](https://losst.ru/kak-udalit-katalog-linux)
- [Копировать файлы по ssh (с хоста на хост/с сервера на сервер) (aposnov.ru)](https://aposnov.ru/%D0%BA%D0%BE%D0%BF%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D1%82%D1%8C-%D1%84%D0%B0%D0%B9%D0%BB%D1%8B-%D0%BF%D0%BE-ssh-%D1%81-%D1%85%D0%BE%D1%81%D1%82%D0%B0-%D0%BD%D0%B0/)