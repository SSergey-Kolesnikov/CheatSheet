[&larr;](readme.md "Ubuntu") Не запускается Apache из-за подвисших процессов
----------------------------------------------------------------------------

После рестарта Apache, он не запускается. Нужно проверить подвисшие процессы и в случае необходимости их завершить.

Проверяем статус Apache:

```markdown
service apache2 status
```

Выводим все процессы Apache и ищем зависший процесс по PID:

```markdown
ps aux | grep apache2
```

Завершаем зависший процесс по PID:

```markdown
kill -9 <PID_APACHE>
```

Перезапускаем Apache:

```markdown
service apache2 restart
```

### Источник

- [Убиваем процессы в Linux — команды ps, kill и killall (pingvinus.ru)](https://pingvinus.ru/note/ps-kill-killall)