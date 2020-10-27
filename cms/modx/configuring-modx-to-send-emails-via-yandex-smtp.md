[&larr;](readme.md "MODX") Настройка MODX для отправки писем через SMTP Яндекса
-------------------------------------------------------------------------------

Список системных настроек MODX, необходимых для отправки писем через SMTP Яндекса.


Имя | Ключ | Значение
--- | --- | :---:
SMTP аутентификация | mail_smtp_auth | Да
Использовать SMTP | mail_use_smtp | Да
SMTP номер порта | mail_smtp_port | 465
SMTP префикс для соединений | mail_smtp_prefix | ssl
SMTP хосты | mail_smtp_hosts | smtp.yandex.ru
SMTP пользователь | mail_smtp_user | \<EMAIL\>
SMTP пароль | mail_smtp_pass | \<PASSWORD\>

где:

- `<EMAIL>` - специально созданный почтовый ящик для рассылок, например `no-reply@mydomain.ru`;
- `<PASSWORD>` - пароль почтового ящика;

## Источник

- [Управление E-mail (modhost.pro)](https://modhost.pro/help/email)