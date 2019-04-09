[&larr;](readme.md "Шпаргалка") MySQL
--------------------------------------

## <a name="content"></a> Содержание:
- [Команды](#commands)
- [Ситуации](#situations)
- [Ссылки](#links)

## <a name="commands"></a> Команды [&uarr;](#content)

#### Статус MySQL
```markdown
service mysql status
```

#### Перезапуск MySQL
```markdown
service mysql restart
```

#### Выводим на экран список процессов MySQL
```markdown
ps aux | grep mysql
```
Команда `ps` предназначена для вывода списка активных процессов в системе и информации о них. 

Команда `grep` запускается одновременно с `ps` (в канале) и будет выполнять поиск по результатам команды `ps` и на экран будут выведены только те строки, которые содержат строку (слово) `mysql`.

#### Завершаем процесс по PID
Команда kill предназначена для посылки сигнала процессу. По умолчанию, если мы не указываем какой сигнал посылать, посылается сигнал SIGTERM (от слова termination — завершение). SIGTERM указывает процессу на то, что необходимо завершиться. Каждый сигнал имеет свой номер. SIGTERM имеет номер 15.
```markdown
kill <PID_MYSQL>
```
Сигнал SIGTERM может и не остановить процесс (например, при перехвате или блокировке сигнала), SIGKILL же выполняет уничтожение процесса всегда, так как его нельзя перехватить или проигнорировать.
```markdown
kill -9 <PID_MYSQL>
```
Список всех сигналов (и их номеров), которые может послать команда kill, можно вывести, выполнив kill -l.

#### Создаем бекап БД MySQL
```markdown
mysqldump -u <USER> -p<PASSWORD> <DATABASE> > "<FILE_NAME>.sql"
```
либо с последующей архивацией бекапа
```markdown
mysqldump -u <USER> -p<PASSWORD> <DATABASE> | gzip > "<FILE_NAME>.sql.gz"
```

## <a name="situations"></a> Ситуации [&uarr;](#content)

#### MySQL не перезапустился
После рестарта MySQL, он не запускается. Нужно проверить подвисшие процессы и в случае необходимости их завершить.
```markdown
service mysql status //Статус MySQL
ps aux | grep mysql //Выводим все процессы MySQL и ищем зависший процесс по PID
kill -9 <PID_MYSQL> //Завершаем процесс по PID
service mysql restart //Перезапуск MySQL
```

## <a name="links"></a> Ссылки [&uarr;](#content)

- [Убиваем процессы в Linux — команды ps, kill и killall](https://pingvinus.ru/note/ps-kill-killall)