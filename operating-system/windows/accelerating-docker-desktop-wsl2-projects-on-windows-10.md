[&larr;](readme.md "Windows") Ускоряем работу проектов на базе Docker Desktop + WSL2 в Windows 10
-------------------------------------------------------------------------------------------------

Docker Desktop + WSL2 в Windows 10 со стандартными настройками работает довольно медленно, ожидание ответа может составлять от 30 до 60 секунд и более. Причина в том, что проект монтируется из файловой системы Windows, а не из собственной файловой системы Linux. Решение - перенести файлы проекта в файловую систему Linux.

Первым делом монтируем сетевой диск на файловую систему Linux, при этом предполагается, что приложение Ubuntu on Windows уже установлено на компьютере. Переходим в проводнике на `Этот компьютер`, далее в меню выбираем `Компьютер` -> `Подключить сетевой диск`. Выбираем для селекта `Диск` букву сетевого диска, к примеру пусть будет `E`, а к полю `Папка` указываем `\\wsl$\Ubuntu`. Теперь в проводнике в разделе `Этот компьютер` будет сетевой диск `Е:` с лейблом `Ubuntu (\\wsl$)`, который ведет на файловую структуру Linux.

Далее создаем проект, в файловой системе Linux. В PhpStorm для создания проекта, к примеру, нажимаем `Get from VCS`. В открывшемся окне в поле `URL` указываем url репозитория, а в поле `Directory` указываем путь к нашему проекту. Путь будет указывать на файловую систему Linux, поэтому выглядеть будет так `<DISK>:\home\<USER>\<PROJECT>`, где `<DISK>` - буква выбранного ранее сетевого диска, `<USER>` - пользователь ОС, `<PROJECT>` - наименование проекта. В моем случае путь получился следующий `E:\home\user\project`.

Теперь необходимо смонтировать контейнеры Docker'а. Для этого запускаем Ubuntu on Windows и переходим в папку проекта командой `cd <PATH>`, где `<PATH>` - путь до проекта. В моем случае команда будет `cd project`. Теперь необходимо запустить монтирование контейнеров Docker'а, для этого выполняем команду `docker-compose -f <PATH_TO_DOCKER_COMPOSE_FILE> up -d --build`, где `<PATH_TO_DOCKER_COMPOSE_FILE>` - путь до файла Docker Compose. В моем случае эта команда выглядит так `docker-compose -f docker/docker-compose-local.yml up -d --build`, т.к. имя файла Docker Compose кастомное под локальную разработку.

В принципе на этом все, ответы сервера на запросы теперь в районе одной или двух секунд.

В дальнейшей работе можно столкнуться с проблемой не настроеных разрешений в файловой системе Linux. К примеру для Laravel проблема может быть в невозможности записи в файловую систему, в таком случае необходимо поменять права на папки `storage` и `bootstrap/cache`. Для этого в приложении Ubuntu on Windows необходимо выполнить следующие команды:

```markdown
user@computer:~/<PROJECT>$ sudo chmod -R 755 storage
```

```markdown
user@computer:~/<PROJECT>$ sudo chmod -R 755 bootstrap/cache
```

где:

- `<PROJECT>` - наименование папки с проектом, откуда запускается команда;

> В случае локальной разработки, права на папки в приложении Ubuntu on Windows можно сразу поставить `777` вместо `755` следующими командами:
>
> ```markdown
> user@computer:~/<PROJECT>$ sudo chmod -R 777 storage
> ```
>
> ```markdown
> user@computer:~/<PROJECT>$ sudo chmod -R 777 bootstrap/cache
> ```
>
> где:
>
> - `<PROJECT>` - наименование папки с проектом, откуда запускается команда;

<a name="sources"></a>
## Источники

- [Fast Docker on Windows in 2022 (createit.com)](https://www.createit.com/blog/make-docker-on-windows-fast-again-2022/)
- [docker on wsl2 very slow (stackoverflow.com)](https://stackoverflow.com/questions/62154016/docker-on-wsl2-very-slow)
- [Docker работает очень медленно при запуске Laravel в контейнере Nginx wsl2 (question-it.com)](https://question-it.com/questions/11663190/docker-rabotaet-ochen-medlenno-pri-zapuske-laravel-v-kontejnere-nginx-wsl2)
- [How to fix Error: laravel.log could not be opened? (stackoverflow.com)](https://stackoverflow.com/a/44647615)
