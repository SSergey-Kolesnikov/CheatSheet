[&larr;](readme.md "Ubuntu") Установка Composer на Ubuntu 16.04
---------------------------------------------------------------

Composer — это пакетный менеджер уровня приложений для языка программирования PHP, который предоставляет средства по управлению зависимостями в PHP-приложении. Composer работает через интерфейс командной строки и устанавливает зависимости (например библиотеки) для приложения.

Обновляем индекс пакетов:

```markdown
sudo apt-get update
```

Переходим в домашний каталог:

```markdown
cd ~
```

Скачиваем установщик при помощи cURL:

```markdown
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

Проверяем, что хэш SHA-384 пакета совпадает с хэшем инсталлятора на [этой странице](https://composer.github.io/pubkeys.html):

```markdown
php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

Результатом запуска команды, если значения совпали, должно быть `Installer verified`.

Запускаем глобальную установку Composer:

```markdown
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Эта команда загрузит пакет менеджера Composer и выполнит его глобальную установку в /usr/local/bin, после чего в системе появится общедоступная команда composer. Вывод будет выглядеть так:

```markdown
All settings correct for using Composer
Downloading...

Composer (version 1.10.7) successfully installed to: /usr/local/bin/composer
Use it: php /usr/local/bin/composer
```

Для того, чтобы убедиться в том, что установка прошла успешно, запускаем команду:

```markdown
composer
```

Результатом выполнения команды будет:

```markdown
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version 1.10.7 2020-06-03 10:03:56
```

Это означает, что Composer был успешно установлен.

## Источник

- [Composer (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Composer)
- [УСТАНОВКА И ИСПОЛЬЗОВАНИЕ COMPOSER В UBUNTU 16.04 (8host.com)](https://www.8host.com/blog/ustanovka-i-ispolzovanie-composer-v-ubuntu-16-04/)
- [Установка Composer на Ubuntu (tyapk.ru)](https://tyapk.ru/blog/post/install-composer-on-ubuntu)