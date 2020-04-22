[&larr;](readme.md "MODX") Подмена конфигурационных файлов MODX при создании копии сайта
----------------------------------------------------------------------------------------

Скрипт необходим для подмены конфигурационных файлов MODX Revolution при создании копии сайта, чтобы каждый раз не прописывать параметры вручную.

Создаем файл `migration.php` в корне сайта, заполняем в нем необходимые параметры и запускаем его из браузера.

```php
<?php

$base_path = __DIR__ . '/';

$params = [];
$params['table_prefix'] = 'modx_';
switch ($_SERVER['HTTP_HOST']) {
    case 'yoursite.ru':
        $params['yoursite.ru'] = 'localhost';
        $params['dbase'] = 'base';
        $params['database_user'] = 'root';
        $params['database_password'] = 'password';
        break;
    case 'dev.yoursite.ru':
        $params['database_server'] = 'localhost';
        $params['dbase'] = 'base_dev';
        $params['database_user'] = 'user';
        $params['database_password'] = 'password';
        break;
    default:
        exit;
}
$params['lastInstallTime'] = time();
$params['site_id'] = 'XXXXXXXXXXXXXXXXXX.XXXXXXXX';
$params['site_sessionname'] = 'XXXXXXXXXXXXXXX';
$params['uuid'] = 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX';
$params['host'] = $_SERVER['HTTP_HOST'];
$params['base_path'] = $base_path;
$params['base_url'] = '/';
$params['core_path'] = $base_path . 'core/';
$params['manager_path'] = $base_path . 'manager/';
$params['manager_url']= '/manager/';
$params['connectors_path'] = $base_path . 'connectors/';
$params['connectors_url'] = '/connectors/';
$params['assets_path'] = $base_path . 'assets/';
$params['assets_url'] = '/assets/';
$params['processors_path'] = $params['core_path'] . 'model/modx/processors/';

$markers = [];
$markers[$params['base_path'] . 'config.core.php'] = 'config';
$markers[$params['connectors_path'] . 'config.core.php'] = 'config';
$markers[$params['manager_path'] . 'config.core.php'] = 'config';
$markers[$params['core_path'] . 'config/config.inc.php'] = 'core_config';

$thisfile = file_get_contents(__FILE__);
foreach ($markers as $path => $marker) {
    preg_match("#.+-----{$marker}-----\r\n(.+)\r\n-----{$marker}-----.+#s", $thisfile, $matches);
    $file = $matches[1];
    foreach ($params as $key=>$value) {
        $file = str_replace("{%{$key}%}", $value, $file);
    }
    file_put_contents($path, $file);
}

removeDirectory($params['core_path'] . 'cache/');

function removeDirectory($path) {
    if (file_exists($path) AND is_dir($path)) {
        $dir = opendir($path);
        while (false !== ($element = readdir($dir))) {
            if ($element != '.' AND $element != '..')  {
                $tmp = $path . '/' . $element;
                if (is_dir($tmp)) {
                    removeDirectory($tmp);
                } else {
                    unlink($tmp);
                }
            }
        }
        closedir($dir);
        if (file_exists($path)) {
            rmdir($path);
        }
    }
}

/* Шаблон файлов config.core.php, лежащих в корне/manager/connectors
-----config-----
<?php

define('MODX_CORE_PATH', '{%core_path%}');
define('MODX_CONFIG_KEY', 'config');
?>
-----config----- */

/* Шаблон файла core.config.inc
-----core_config-----
<?php

$database_type = 'mysql';
$database_server = '{%database_server%}';
$database_user = '{%database_user%}';
$database_password = '{%database_password%}';
$database_connection_charset = 'utf8';
$dbase = '{%dbase%}';
$table_prefix = '{%table_prefix%}';
$database_dsn = 'mysql:host={%database_server%};dbname={%dbase%};charset=utf8';
$config_options = array (
);
$driver_options = array (
);

$lastInstallTime = {%lastInstallTime%};

$site_id = '{%site_id%}';
$site_sessionname = '{%site_sessionname%}';
$https_port = '443';
$uuid = '{%uuid%}';

if (!defined('MODX_CORE_PATH')) {
    $modx_core_path= '{%core_path%}';
    define('MODX_CORE_PATH', $modx_core_path);
}
if (!defined('MODX_PROCESSORS_PATH')) {
    $modx_processors_path= '{%processors_path%}';
    define('MODX_PROCESSORS_PATH', $modx_processors_path);
}
if (!defined('MODX_CONNECTORS_PATH')) {
    $modx_connectors_path= '{%connectors_path%}';
    $modx_connectors_url= '{%connectors_url%}';
    define('MODX_CONNECTORS_PATH', $modx_connectors_path);
    define('MODX_CONNECTORS_URL', $modx_connectors_url);
}
if (!defined('MODX_MANAGER_PATH')) {
    $modx_manager_path= '{%manager_path%}';
    $modx_manager_url= '{%manager_url%}';
    define('MODX_MANAGER_PATH', $modx_manager_path);
    define('MODX_MANAGER_URL', $modx_manager_url);
}
if (!defined('MODX_BASE_PATH')) {
    $modx_base_path= '{%base_path%}';
    $modx_base_url= '{%base_url%}';
    define('MODX_BASE_PATH', $modx_base_path);
    define('MODX_BASE_URL', $modx_base_url);
}
if(defined('PHP_SAPI') && (PHP_SAPI == "cli" || PHP_SAPI == "embed")) {
    $isSecureRequest = false;
} else {
    $isSecureRequest = ((isset($_SERVER['HTTPS']) && !empty($_SERVER['HTTPS']) && strtolower($_SERVER['HTTPS']) !== 'off') || $_SERVER['SERVER_PORT'] == $https_port);
}
if (!defined('MODX_URL_SCHEME')) {
    $url_scheme=  $isSecureRequest ? 'https://' : 'http://';
    define('MODX_URL_SCHEME', $url_scheme);
}
if (!defined('MODX_HTTP_HOST')) {
    if(defined('PHP_SAPI') && (PHP_SAPI == "cli" || PHP_SAPI == "embed")) {
        $http_host='{%host%}';
        define('MODX_HTTP_HOST', $http_host);
    } else {
        $http_host= array_key_exists('HTTP_HOST', $_SERVER) ? htmlspecialchars($_SERVER['HTTP_HOST'], ENT_QUOTES) : '{%host%}';
        if ($_SERVER['SERVER_PORT'] != 80) {
            $http_host= str_replace(':' . $_SERVER['SERVER_PORT'], '', $http_host); // remove port from HTTP_HOST
        }
        $http_host .= ($_SERVER['SERVER_PORT'] == 80 || $isSecureRequest) ? '' : ':' . $_SERVER['SERVER_PORT'];
        define('MODX_HTTP_HOST', $http_host);
    }
}
if (!defined('MODX_SITE_URL')) {
    $site_url= $url_scheme . $http_host . MODX_BASE_URL;
    define('MODX_SITE_URL', $site_url);
}
if (!defined('MODX_ASSETS_PATH')) {
    $modx_assets_path= '{%assets_path%}';
    $modx_assets_url= '{%assets_url%}';
    define('MODX_ASSETS_PATH', $modx_assets_path);
    define('MODX_ASSETS_URL', $modx_assets_url);
}
if (!defined('MODX_LOG_LEVEL_FATAL')) {
    define('MODX_LOG_LEVEL_FATAL', 0);
    define('MODX_LOG_LEVEL_ERROR', 1);
    define('MODX_LOG_LEVEL_WARN', 2);
    define('MODX_LOG_LEVEL_INFO', 3);
    define('MODX_LOG_LEVEL_DEBUG', 4);
}

-----core_config-----*/
```

### Источник

- [Скрипт подмены конфигов сайта на лету (modx.pro)](https://modx.pro/solutions/19107)