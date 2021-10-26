[&larr;](readme.md "SSH команды") Composer
------------------------------------------

#### Текущая версия

```markdown
user@computer:~$ composer
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 2.0.13 2021-04-27 13:11:08
...
```

#### Просмотр списка устаревших библиотек

```markdown
user@computer:~$ composer show -l
asm89/stack-cors                   v2.0.3  v2.0.3  Cross-origin resource sharing library and stack middleware
bacon/bacon-qr-code                2.0.4   2.0.4   BaconQrCode is a QR code generator for PHP.
barryvdh/laravel-debugbar          v3.6.2  v3.6.2  PHP Debugbar integration for Laravel
brick/math                         0.9.2   0.9.3   Arbitrary-precision arithmetic library
...
```

#### Очистка кеша

```markdown
user@computer:~$ composer clearcache
Cache directory does not exist (cache-vcs-dir): 
Clearing cache (cache-repo-dir): /home/user/.cache/composer/repo
Clearing cache (cache-files-dir): /home/user/.cache/composer/files
Clearing cache (cache-dir): /home/user/.cache/composer
All caches cleared.
```

## <a name="sources"></a> Источники

- [Как обновить библиотеки в файле composer.json до актуальных версий (evilinside.ru)](https://evilinside.ru/kak-obnovit-biblioteki-v-fajle-composer-json-do-aktualnyx-versij/)
- [Как изменить версию composer: обновиться или откатиться на старую версию (badcode.ru)](https://badcode.ru/kak-izmienit-viersiiu-composer-obnovitsia-ili-otkatitsia-na-staruiu-viersiiu/)