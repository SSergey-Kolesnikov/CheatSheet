[&larr;](readme.md "Шпаргалка") Apache
--------------------------------------

## <a name="content"></a> Содержание:
- [Команды](#commands)
- [Ситуации](#situations)
- [Ссылки](#links)

## <a name="commands"></a> Команды [&uarr;](#content)

#### Статус Apache
```markdown
service apache2 status
```

#### Запуск Apache
```markdown
service apache2 start
```

#### Перезапуск Apache
```markdown
service apache2 restart
```

#### Остановка Apache
```markdown
service apache2 stop
```

#### Выводим на экран список процессов Apache
```markdown
ps aux | grep apache2
```
Команда `ps` предназначена для вывода списка активных процессов в системе и информации о них. 

Команда `grep` запускается одновременно с `ps` (в канале) и будет выполнять поиск по результатам команды `ps` и на экран будут выведены только те строки, которые содержат строку (слово) `apache2`.

#### Завершаем процесс по PID
Команда kill предназначена для посылки сигнала процессу. По умолчанию, если мы не указываем какой сигнал посылать, посылается сигнал SIGTERM (от слова termination — завершение). SIGTERM указывает процессу на то, что необходимо завершиться. Каждый сигнал имеет свой номер. SIGTERM имеет номер 15.
```markdown
kill <PID_APACHE>
```
Сигнал SIGTERM может и не остановить процесс (например, при перехвате или блокировке сигнала), SIGKILL же выполняет уничтожение процесса всегда, так как его нельзя перехватить или проигнорировать.
```markdown
kill -9 <PID_APACHE>
```
Список всех сигналов (и их номеров), которые может послать команда kill, можно вывести, выполнив kill -l.

## <a name="situations"></a> Ситуации [&uarr;](#content)

#### Apache не перезапустился
После рестарта Apache, он не запускается. Нужно проверить подвисшие процессы и в случае необходимости их завершить.
```markdown
service apache2 status //Статус Apache
ps aux | grep apache2 //Выводим все процессы Apache и ищем зависший процесс по PID
kill -9 <PID_APACHE> //Завершаем процесс по PID
service apache2 restart //Перезапуск Apache
```

## <a name="links"></a> Ссылки [&uarr;](#content)

- [Убиваем процессы в Linux — команды ps, kill и killall](https://pingvinus.ru/note/ps-kill-killall)