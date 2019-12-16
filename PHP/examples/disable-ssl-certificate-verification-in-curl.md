[&larr;](readme.md "Примеры") Отключение проверки SSL-сертификата в cURL
------------------------------------------------------------------------

При получении DOM дерева с помощью cURL, к примеру при истекшем сроке действия SSL-сертификата, по умолчанию выводится ошибка. Для корректного получения необходимо установить параметр для сеанса cURL `CURLOPT_SSL_VERIFYPEER` в значение false.

`CURLOPT_SSL_VERIFYPEER` — FALSE для остановки cURL от проверки сертификата узла сети. Альтернативные сверяемые сертификаты могут быть указаны с помощью параметра `CURLOPT_CAINFO` или директории с сертификатами, указываемой параметром `CURLOPT_CAPATH`. По умолчанию равно TRUE, начиная с версии cURL 7.10.

```php
$params = array(
	CURLOPT_URL => $url,
	CURLOPT_AUTOREFERER => true,
	CURLOPT_RETURNTRANSFER => true,
	CURLOPT_HEADER => false,
	CURLOPT_CONNECTTIMEOUT => 120,
	CURLOPT_TIMEOUT => 120,
	CURLOPT_MAXREDIRS => 10,
	CURLOPT_FOLLOWLOCATION => false,
	CURLOPT_NOBODY => false,
	CURLOPT_USERAGENT => "Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US) AppleWebKit/530.5 (KHTML, like Gecko) Chrome/2.0.172.39 Safari/530.5",
	CURLOPT_SSL_VERIFYPEER => false,
);
```

### Источник

- [PHP: curl_setopt (php.net)](https://www.php.net/manual/ru/function.curl-setopt.php)