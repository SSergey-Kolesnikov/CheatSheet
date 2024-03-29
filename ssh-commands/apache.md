[&larr;](readme.md "SSH команды") Apache
----------------------------------------

#### Статус Apache

```markdown
user@computer:~$ systemctl status apache2
```

```markdown
user@computer:~$ service apache2 status
```

#### Запуск Apache

```markdown
user@computer:~$ systemctl start apache2
```

```markdown
user@computer:~$ service apache2 start
```

#### Перезапуск Apache

```markdown
user@computer:~$ systemctl restart apache2
```

```markdown
user@computer:~$ service apache2 restart
```

#### Остановка Apache

```markdown
user@computer:~$ systemctl stop apache2
```

```markdown
user@computer:~$ service apache2 stop
```

#### Выводим на экран список процессов Apache

```markdown
user@computer:~$ ps aux | grep apache2
```

Команда `ps` предназначена для вывода списка активных процессов в системе и информации о них. 

Команда `grep` запускается одновременно с `ps` (в канале) и будет выполнять поиск по результатам команды `ps` и на экран будут выведены только те строки, которые содержат строку (слово) `apache2`.

#### Завершаем процесс по PID

Команда kill предназначена для посылки сигнала процессу. По умолчанию, если мы не указываем какой сигнал посылать, посылается сигнал SIGTERM (от слова termination — завершение). SIGTERM указывает процессу на то, что необходимо завершиться. Каждый сигнал имеет свой номер. SIGTERM имеет номер 15.

```markdown
user@computer:~$ kill <PID_APACHE>
```

Сигнал SIGTERM может и не остановить процесс (например, при перехвате или блокировке сигнала), SIGKILL же выполняет уничтожение процесса всегда, так как его нельзя перехватить или проигнорировать.

```markdown
user@computer:~$ kill -9 <PID_APACHE>
```

Список всех сигналов (и их номеров), которые может послать команда kill, можно вывести, выполнив kill -l.

## Источник

- [Убиваем процессы в Linux — команды ps, kill и killall (pingvinus.ru)](https://pingvinus.ru/note/ps-kill-killall)