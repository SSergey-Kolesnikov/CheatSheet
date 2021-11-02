[&larr;](readme.md "SSH команды") Git
-------------------------------------

## <a name="content"></a> Содержание:

- [Команды](#commands)
    - [Настройки](#commands_settings)
    - [Репозитории](#commands_repositories)
    - [Ветки](#commands_branches)
    - [Коммиты](#commands_commits)
    - [Прочее](#commands_other)
- [Ситуации](#situations)
- [Источники](#sources)

## <a name="commands"></a> Команды

### <a name="commands_settings"></a> Настройки

#### Вывод параметров Git'а

```markdown
git config --list
```

#### Установка параметров Git'а

Глобальные настройки локального репозитория, email:

```markdown
git config --global user.email "<YOUR_EMAIL>"
```

Глобальные настройки локального репозитория, имя пользователя:

```markdown
git config --global user.name "<YOUR_NAME>"
```

Локальные настройки локального репозитория, email:

```markdown
git config --local user.email "<YOUR_EMAIL>"
```

Локальные настройки локального репозитория, имя пользователя:

```markdown
git config --local user.name "<YOUR_NAME>"
```

### <a name="commands_repositories"></a> Репозитории

#### Создаем пустой локальный Git-репозиторий

```markdown
git init
```

#### Клонируем удаленный репозиторий

```markdown
git clone <LINK>
```

После клонирования репозитория, в текущей папке создается папка с названием репозитория и все файлы лежат уже в ней.

```markdown
git clone <LINK> ./
```

После клонирования репозитория, все файлы репозитория создаются в текущей папке, но она предварительно должна быть пустой.

#### Добавляем удаленный репозиторий (главный)

```markdown
git remote add origin <LINK>
```

#### Перепривязываем удаленный репизиторий (главный)

```markdown
git remote set-url origin <LINK>
```

### <a name="commands_branches"></a> Ветки

#### Создание веток

Только создание локальной ветки:

```markdown
git branch <BRANCH_NAME>
```

Создание локальной ветки и переключение на нее:

```markdown
git checkout -b <BRANCH_NAME>
```

Создание локальной ветки `<BRANCH_NAME_1>` и связывание с удаленной веткой `<BRANCH_NAME_2>`:

```markdown
git checkout --track -b <BRANCH_NAME_1> origin/<BRANCH_NAME_2>
```

#### Просмотр веток

Только локальные:

```markdown
git branch
```

Только удаленные:

```markdown
git branch -r
```

Все ветки (локальные + удаленные):

```markdown
git branch -a
```

#### Переключение на ветку `<BRANCH_NAME>`

```markdown
git checkout <BRANCH_NAME>
```

#### Привязываем локальную ветку `<BRANCH_NAME_1>` к удаленной ветке `<BRANCH_NAME_2>`

```markdown
git branch --set-upstream <BRANCH_NAME_1> origin/<BRANCH_NAME_2>
```

#### Слияние веток

Слияние текущей локальной ветки с локальной веткой `<BRANCH_NAME>`:

```markdown
git merge <BRANCH_NAME>
```

Слияние текущей локальной ветки с локальной веткой `<BRANCH_NAME>` (без редактора):

```markdown
git merge --no-edit <BRANCH_NAME>
```

#### Переименование веток

Переименование локальной ветки:

```markdown
git branch -m <OLD_BRANCH> <NEW_BRANCH>
```

#### Удаление веток

Локальной ветки:

```markdown
git branch -D <BRANCH_NAME>
```

Удаленной ветки:

```markdown
git push origin --delete <BRANCH_NAME>
```
```markdown
git push origin :<BRANCH_NAME>
```

### <a name="commands_commits"></a> Коммиты

#### Добавление в индекс

Файл или группу файлов:

```markdown
git add .
```

Измененные и новые и удаляет из индекса удаленные файлы:

```markdown
git add -u
```

Все изменения

```markdown
git add -A
```

#### Отмена индекации

```markdown
git checkout <FILE_NAME>
```

Отменяет изменения в указанном файле до индексации (`git add <FILE_NAME>`).

#### Удаление из индекса

Файл из репозитория и с сервера

```markdown
git rm <FILE_NAME>
```

Файл из репозитория без его физического удаления с сервера

```markdown
git rm --cached <FILE_NAME>
```

Папки из локального репозитория

```markdown
git rm -r <FOLDER_NAME>
```

#### Добавление коммита

Добавление коммита с комментарием `<COMMENT>`:

```markdown
git commit -m "<COMMENT>"
```

Добавление изменений в индекс + добавление коммита с комментарием `<COMMENT>`:

```markdown
git commit -a -m "<COMMENT>"
```

#### Редактирование коммита

Измение комментария для последнего коммита (если он не отправлен в origin-репозиторий командой `git push`):

```markdown
git commit --amend -m "<NEW_COMMENT>"
```

#### Отмена коммита

Отмена последнего коммита, но не изменения, которые вы внесли (они сохранятся):

```markdown
git reset --soft HEAD^
```

Отмена последнего коммита, файлы принимают изначальное состояние, изменения удаляются:

```markdown
git revert HEAD --no-edit
```

Жесткая отмена коммита по хэшу (осторожно):

```markdown
git reset --hard <HASH>
```

#### Вталкиваем коммиты

Все ветки:

```markdown
git push origin
```

Текущая ветка в удаленную ветку `<BRANCH_NAME>`:

```markdown
git push origin <BRANCH_NAME>
```

Текущая ветка для создания удаленной ветки `<BRANCH_NAME>` (первый раз для создания удаленной ветки и связывании локальной и удаленной веток):

```markdown
git push -u origin <BRANCH_NAME>
```

Текущая ветка для создания удаленной ветки `<BRANCH_NAME>` (после удаления, когда обычный `push` ругается):

```markdown
git push -f origin <BRANCH_NAME>
```

Текущая ветка с созданием на сервере удаленной ветки `<BRANCH_NAME>`:

```markdown
git push --set-upstream origin <BRANCH_NAME>
```

#### Скачиваем коммиты

С удаленной ветки `<BRANCH_NAME>` в текущую локальную ветку:

```markdown
git pull origin <BRANCH_NAME>
```

С удаленной ветки `<BRANCH_NAME>` в текущую локальную ветку (без комментария при проблемах с объединением):

```markdown
git pull --no-edit origin <BRANCH_NAME>
```

#### История коммитов

Последние `<NUMBER>` коммитов

```markdown
git log -<NUMBER>
```

Cокращенно в одну строку:

```markdown
git log --pretty=oneline
```

Изображенных деревом:

```markdown
git log --graph --all
```

#### Просмотр коммита по хэшу

```markdown
git show <HASH>
```

### <a name="commands_other"></a> Прочее

#### Статусы

Общий:

```markdown
git status
```

Список не отслеживаемых файлов:

```markdown
git status -u
```

#### Просмотр локальной истории

```markdown
git reflog
```

#### Просмотр изменений по файлам

Во всех файлах:

```markdown
git diff
```

В определенном файле:

```markdown
git diff <FILE_NAME>
```

#### Обновление локального состояния

```markdown
git fetch -p
```

К примеру можно использовать после того, как кто-то удалил удаленную ветку, а в локальном репозитории она еще отображается.

#### Просмотр версии Git'а

```markdown
git --version
```

## <a name="situations"></a> Ситуации

## Переименование веток (локальная + удаленная)
- [[Git] Переименование ветки (локально и удаленно) (bulkin.me)](https://bulkin.me/notes/3783)

```markdown
git branch -m <OLD_BRANCH> <NEW_BRANCH> //Переименование локальной ветки    
git push origin :<OLD_BRANCH> //Удаление удаленной ветки
git push --set-upstream origin <NEW_BRANCH> //Вталкивание данных текущей ветки, при этом создавая удаленную ветку и связывая их
```

## Ошибка "git fatal: unable to create thread: Resource temporarily unavailable"

- [Настройка git fatal: unable to create thread: Resource temporarily unavailable) (aposnov.ru)](https://aposnov.ru/%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-git-fatal-unable-to-create-thread-resource-temporarily-unavailable/)

При попытке запушить, вываливается ошибка

```markdown
user@computer:~$ git push -u origin master
Username for 'https://github.com': <USER>
Password for 'https://<USER>@github.com':
Counting objects: 57839, done.
Delta compression using up to 48 threads.
fatal: unable to create thread: Resource temporarily unavailable
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
error: failed to push some refs to 'https://github.com/<USER>/<REPOSITORY>.git'
fatal: write error: Bad file descriptor
```

где:

- `<USER>` - имя пользователя на [GitHub](https://github.com/);
- `<REPOSITORY>` - наименование репозитория на [GitHub](https://github.com/);

Добавляем настройки для Git'а

```markdown
user@computer:~$ git config --local pack.windowMemory 100m
```

```markdown
user@computer:~$ git config --local pack.packSizeLimit 100m
```

```markdown
user@computer:~$ git config --local pack.threads 1
```

Проверяем, применились ли настройки

```markdown
user@computer:~$ git config --list
...
pack.windowmemory=100m
pack.packsizelimit=100m
pack.threads=1
```

И повторно пушим коммиты на [GitHub](https://github.com/)

```markdown
user@computer:~$ git push -u origin master
Username for 'https://github.com': <USER>
Password for 'https://<USER>@github.com':
Counting objects: 57839, done.
Compressing objects: 100% (52256/52256), done.
Writing objects: 100% (57839/57839), 305.32 MiB | 11.90 MiB/s, done.
Total 57839 (delta 6839), reused 0 (delta 0)
remote: Resolving deltas: 100% (6839/6839), done.
To https://github.com/<USER>/<REPOSITORY>.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

где:

- `<USER>` - имя пользователя на [GitHub](https://github.com/);
- `<REPOSITORY>` - наименование репозитория на [GitHub](https://github.com/);

## <a name="sources"></a> Источники

- [Git - Book (git-scm.com)](https://git-scm.com/book/ru/v2)
- [Часто используемые команды Git (bulkin.me)](https://bulkin.me/notes/3298)
- [Git — Удалить Ветку (Локальную или Удаленную) (shellhacks.com)](https://www.shellhacks.com/ru/git-delete-branch-local-remote/)