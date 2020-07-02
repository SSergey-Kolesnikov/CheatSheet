[&larr;](readme.md "Ubuntu") Не запускается MySQL из-за подвисших процессов
---------------------------------------------------------------------------

После рестарта MySQL, он не запускается. Нужно проверить подвисшие процессы и в случае необходимости их завершить.

Проверяем статус MySQL:

```markdown
service mysql status
```

Выводим все процессы MySQL и ищем зависший процесс по PID:

```markdown
ps aux | grep mysql
```

Завершаем зависший процесс по PID:

```markdown
kill -9 <PID_MYSQL>
```

Перезапускаем MySQL:

```markdown
service mysql restart
```

### Источник

- [Убиваем процессы в Linux — команды ps, kill и killall (pingvinus.ru)](https://pingvinus.ru/note/ps-kill-killall)