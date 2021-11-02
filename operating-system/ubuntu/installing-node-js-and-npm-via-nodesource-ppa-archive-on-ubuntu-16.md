[&larr;](readme.md "Ubuntu") Установка Node.js и npm через архив PPA NodeSource на Ubuntu 16
--------------------------------------------------------------------------------------------

> Node.js — программная платформа, основанная на движке V8 (транслирующем JavaScript в машинный код), превращающая JavaScript из узкоспециализированного языка в язык общего назначения. Node.js добавляет возможность JavaScript взаимодействовать с устройствами ввода-вывода через свой API, написанный на C++, подключать другие внешние библиотеки, написанные на разных языках, обеспечивая вызовы к ним из JavaScript-кода.

> npm (Node Package Manager) - менеджер пакетов, входящий в состав Node.js.

## <a name="content"></a> Содержание:

- [Скачиваем архив PPA](#download-the-ppa-nodesource-archive)
- [Устанавливаем через пакетный менеджер](#install-via-the-package-manager)
- [Проверяем версию Node.js](#checking-the-node-js-version)
- [Проверяем версию npm](#checking-the-npm-version)
- [Источники](#sources)

## <a name="download-the-ppa-nodesource-archive"></a> Скачиваем архив PPA NodeSource [&uarr;](#content "Содержание")

Номер последней версии для Node.js можно найти в документации по [NodeSource](https://github.com/nodesource/distributions#debinstall). На текущий момент это версия 17.

```markdown
user@computer:~$ curl -fsSL https://deb.nodesource.com/setup_17.x | sudo -E bash -

## Installing the NodeSource Node.js 17.x repo...
...
## Run `sudo apt-get install -y nodejs` to install Node.js 17.x and npm
## You may also need development tools to build native addons:
     sudo apt-get install gcc g++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null
     echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn

```

## <a name="install-via-the-package-manager"></a> Устанавливаем через пакетный менеджер [&uarr;](#content "Содержание")

```markdown
user@computer:~$ sudo apt-get install -y nodejs
Reading package lists... Done
...
Unpacking nodejs (17.0.1-1nodesource1) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up nodejs (17.0.1-1nodesource1) ...
```

> Пакет [NodeSource](https://github.com/nodesource/distributions) `nodejs` содержит двоичный код `node` и `npm`, так что не нужно устанавливать `npm` отдельно.

## <a name="checking-the-node-js-version"></a> Проверяем версию Node.js [&uarr;](#content "Содержание")

```markdown
user@computer:~$ node -v
v17.0.1
```

## <a name="checking-the-npm-version"></a> Проверяем версию npm [&uarr;](#content "Содержание")

```markdown
user@computer:~$ npm -v
8.1.0
```

## <a name="sources"></a> Источники [&uarr;](#content "Содержание")

- [NodeSource Node.js Binary Distributions (github.com)](https://github.com/nodesource/distributions)
- [Установка Node.js в Ubuntu 20.04 (digitalocean.com)](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04-ru)
- [Как Установить Node.js и NPM в Ubuntu 18.04 (hostinger.ru)](https://www.hostinger.ru/rukovodstva/kak-ustanovit-node-js-npm-ubuntu)
- [Node.js (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Node.js)
- [npm (ru.wikipedia.org)](https://ru.wikipedia.org/wiki/Npm)