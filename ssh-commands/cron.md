[&larr;](readme.md "SSH команды") Cron
--------------------------------------

#### Просмотр задач

```markdown
user@computer:~$ crontab -l
0 3 1 * * /usr/bin/apt-get update
```

где:

- `0 3 1 * * /usr/bin/apt-get update` - запуск обновлений пакетов с помощью пакетного менеджера apt каждый месяц 1го числа в 03:00;

#### Редактирование задач

```markdown
user@computer:~$ crontab -e
```

После запуска команды `crontab -e` открывается редактор текста, который назначен в ОС по-умолчанию.

```markdown
...
<MINUTE> <HOUR> <DAY> <MONTH> <DAY_OF_WEEK> <COMMAND>
...
```

где:

- `<MINUTE>` - минута, указывается число (0 - 59) или символ `*`;
- `<HOUR>` - час, указывается число (0 - 23) или символ `*`;
- `<DAY>` - день, указывается число (1 - 31) или символ `*`;
- `<MONTH>` - месяц, указывается число (1 - 12) или символ `*`;
- `<DAY_OF_WEEK>` - день недели, указывается число (0 - 6) или символ `*`;
- `<COMMAND>` - команда, которую необходимо запустить;

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [Настройка Cron (losst.ru)](https://losst.ru/nastrojka-cron)
- [Cron: что это такое и как его правильно использовать (timeweb.com)](https://timeweb.com/ru/community/articles/chto-takoe-cron)