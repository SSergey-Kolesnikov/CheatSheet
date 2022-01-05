[&larr;](readme.md "Windows") Подключение к удаленному серверу по SSH с использованием ключа через PuTTY
--------------------------------------------------------------------------------------------------------

<a name="content"></a>
## Содержание

- [Заключение](#generating-keys)
- [Размещение ключа на сервере](#placing-the-key-on-the-server)
- [Настройка PuTTY](#setting-up-putty)
- [Заключение](#conclusion)
- [Источники](#sources)

<a name="generating-keys"></a>
## Генерация ключей

Для генерации ключей используем утилиту PuTTYgen. Нажимаем кнопку `Gengerate` и водим курсором мыши по окну приложения до окончания генерации. 

После завершения генерации ключа, в поле `Key comment` можно указать произвольный комментарий для ключей. 

Далее сохраняем себе на компьютер приватный ключ, кликнув по кнопке `Save private key`, его мы далее укажем в настройках PuTTY. А из окна `Public key for pasting into OpenSSH authorized_keys file` копируем в буфер обмена публичный ключ, далее мы его пропишем на сервере.

<a name="placing-the-key-on-the-server"></a>
## Размещение ключа на сервере

На удаленном сервере размещается публичный ключ. Создаем на сервере папку и файл для хранения ключей, а также ограничиваем к ним доступ (получить его может только владелец).

```markdown
user@computer:~$ mkdir ~/.ssh
```

```markdown
user@computer:~$ chmod 0700 ~/.ssh
```

```markdown
user@computer:~$ touch ~/.ssh/authorized_keys
```

```markdown
user@computer:~$ chmod 0644 ~/.ssh/authorized_keys
```

Командой `cat > .ssh/authorized_keys` добавляем публичный ключ в файл `.ssh/authorized_keys`. После ввода команды кликаем по окну терминала правой кнопкой мыши для вставки текста из буфера обмена и для завершения ввода нажимаем Ctrl+D.

<a name="setting-up-putty"></a>
## Настройка PuTTY

В PuTTY указывается приватный ключ, ранее сохраненный на компьютере. В разделе `Connection -> SSH -> Auth` для поля `Private key file for authentication` кликаем по кнопке `Browse` и выбираем ранее сохраненный файл приватного ключа.

<a name="conclusion"></a>
## Заключение

Теперь к серверу через SSH можно подключиться без пароля, достаточно указать логин и IP-адрес сервера.

<a name="sources"></a>
## Источники

- [Как подключиться к серверу по SSH с помощью пароля или ключа (timeweb.com)](https://timeweb.com/ru/community/articles/kak-podklyuchitsya-k-serveru-cherez-ssh-po-parolyu-ili-klyuchu)