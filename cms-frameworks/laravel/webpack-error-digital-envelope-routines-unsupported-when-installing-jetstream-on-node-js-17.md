[&larr;](readme.md "Laravel") Ошибка webpack `digital envelope routines::unsupported` при установке Jetstream на Node.js 17
---------------------------------------------------------------------------------------------------------------------------

При установке Jetstream для Laravel и запуске команды `npm install && npm run dev` на Node.js 17 не LTS версии, возникает ошибка webpack `error:0308010C:digital envelope routines::unsupported`.

```markdown
user@computer:~$ npm install && npm run dev
....
[webpack-cli] Error: error:0308010C:digital envelope routines::unsupported
    at new Hash (node:internal/crypto/hash:67:19)
    at Object.createHash (node:crypto:130:10)
    at BulkUpdateDecorator.hashFactory (/<PATH>/node_modules/webpack/lib/util/createHash.js:155:18)
    at BulkUpdateDecorator.digest (/<PATH>/node_modules/webpack/lib/util/createHash.js:80:21)
    at /<PATH>/node_modules/webpack/lib/DefinePlugin.js:595:38
    at Hook.eval [as call] (eval at create (/<PATH>/node_modules/tapable/lib/HookCodeFactory.js:19:10), <anonymous>:194:1)
    at Hook.CALL_DELEGATE [as _call] (/<PATH>/node_modules/tapable/lib/Hook.js:14:14)
    at Compiler.newCompilation (/<PATH>/node_modules/webpack/lib/Compiler.js:1053:26)
    at /<PATH>/node_modules/webpack/lib/Compiler.js:1097:29
    at Hook.eval [as callAsync] (eval at create (/<PATH>/node_modules/tapable/lib/HookCodeFactory.js:33:10), <anonymous>:22:1) {
  opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
}
```

где:

- `<PATH>` - абсолютный путь до проекта с Laravel;

Есть обходной вариант, добавляем `export NODE_OPTIONS=--openssl-legacy-provider` в файл `/package.json` для `"development": "mix",`.

Меняем

```json
    "scripts": {
        ...
        "development": "mix",
       ...
    },
```

на

```json
    "scripts": {
        ...
        "development": "export SET NODE_OPTIONS=--openssl-legacy-provider && mix",
       ...
    },
```

> #### Исходный файл
> 
> ```json
> {
>     "private": true,
>     "scripts": {
>         "dev": "npm run development",
>         "development": "mix",
>         "watch": "mix watch",
>         "watch-poll": "mix watch -- --watch-options-poll=1000",
>         "hot": "mix watch --hot",
>         "prod": "npm run production",
>         "production": "mix --production"
>     },
>     "devDependencies": {
>         "@tailwindcss/forms": "^0.3.1",
>         "@tailwindcss/typography": "^0.4.0",
>         "alpinejs": "^3.0.6",
>         "axios": "^0.21",
>         "laravel-mix": "^6.0.6",
>         "lodash": "^4.17.19",
>         "postcss": "^8.1.14",
>         "postcss-import": "^14.0.1",
>         "tailwindcss": "^2.2.2"
>     }
> }
> ```
> 
> #### Измененный файл
> 
> ```json
> {
>     "private": true,
>     "scripts": {
>         "dev": "npm run development",
>         "development": "export SET NODE_OPTIONS=--openssl-legacy-provider && mix",
>         "watch": "mix watch",
>         "watch-poll": "mix watch -- --watch-options-poll=1000",
>         "hot": "mix watch --hot",
>         "prod": "npm run production",
>         "production": "mix --production"
>     },
>     "devDependencies": {
>         "@tailwindcss/forms": "^0.3.1",
>         "@tailwindcss/typography": "^0.4.0",
>         "alpinejs": "^3.0.6",
>         "axios": "^0.21",
>         "laravel-mix": "^6.0.6",
>         "lodash": "^4.17.19",
>         "postcss": "^8.1.14",
>         "postcss-import": "^14.0.1",
>         "tailwindcss": "^2.2.2"
>     }
> }
> ```

Далее удаляем папку `node_modules`, файлы `package-lock.json` и `yarn.lock`, сбрасываем кеш у npm и заново запускаем установку npm-пакетов. Выполняем последовательно следующие команды.

```markdown
user@computer:~$ rm -rf node_modules
```

```markdown
user@computer:~$ rm package-lock.json yarn.lock
```

```markdown
user@computer:~$ npm cache clear --force
npm WARN using --force Recommended protections disabled.
```

```markdown
user@computer:~$ npm install && npm run dev
npm WARN deprecated querystring@0.2.0: The querystring API is considered Legacy. new code should use the URLSearchParams API instead.
npm WARN deprecated uuid@3.4.0: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.

added 811 packages, and audited 812 packages in 31s

87 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

> dev
> npm run development


> development
> export SET NODE_OPTIONS=--openssl-legacy-provider && mix


● Mix █████████████████████████ emitting (98%)
 after emit


warn - You have enabled the JIT engine which is currently in preview.
warn - Preview features are not covered by semver, may introduce breaking changes, and can change at any time.



● Mix █████████████████████████ done (99%) plugins
 WebpackBar:done


warn - You have enabled the JIT engine which is currently in preview.
warn - Preview features are not covered by semver, may introduce breaking changes, and can change at any time.


✔ Mix
  Compiled successfully in 2.84s


warn - You have enabled the JIT engine which is currently in preview.
warn - Preview features are not covered by semver, may introduce breaking changes, and can change at any time.


   Laravel Mix v6.0.34


✔ Compiled Successfully in 2794ms
┌─────────────────────────────────────────────────────────────────────────────────────────────────┬──────────┐
│                                                                                            File │ Size     │
├─────────────────────────────────────────────────────────────────────────────────────────────────┼──────────┤
│                                                                                      /js/app.js │ 707 KiB  │
│                                                                                     css/app.css │ 42.9 KiB │
└─────────────────────────────────────────────────────────────────────────────────────────────────┴──────────┘
webpack compiled successfully
```

## <a name="sources"></a> Источники

- [nodejs 17: digital envelope routines::unsupported (github.com)](https://github.com/webpack/webpack/issues/14532)
- [nodejs 17: digital envelope routines::unsupported, комментарий akornatskyy (github.com)](https://github.com/webpack/webpack/issues/14532#issuecomment-947012063)
- [nodejs 17: digital envelope routines::unsupported, комментарий DevlinRocha (github.com)](https://github.com/webpack/webpack/issues/14532#issuecomment-951378874)
- [Laravel 7 npm run dev give error required webpack-cli when install give error (laracasts.com)](https://laracasts.com/discuss/channels/laravel/laravel-7-npm-run-dev-give-error-required-webpack-cli-when-install-give-error)