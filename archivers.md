[&larr;](readme.md "Шпаргалка") Архиваторы
--------------------------------------

## <a name="content"></a> Содержание:
- [Команды](#commands)
    - [Gzip](#commands_gzip)
    - [Zip](#commands_zip)

## <a name="commands"></a> Команды [&uarr;](#content)

### <a name="commands_gzip"></a> Gzip [&uarr;](#content)

#### Архивируем папку
```markdown
tar -zcvf "<FILE_NAME>.tar.gz" <PATH>/
```

#### Архивируем все внутри текущей папки
```markdown
tar -zcvf "<FILE_NAME>.tar.gz" *
```

#### Архивируем все внутри текущей папки (включая скрытые файлы)
```markdown
tar -zcvf "<FILE_NAME>.tar.gz" .
```

#### Разархивируем в текущую папку
```markdown
tar -xzvf "<FILE_NAME>"
```

### <a name="commands_zip"></a> Zip [&uarr;](#content)

#### Архивируем все внутри текущей папки
```markdown
zip -r "<FILE_NAME>.zip" *
```
#### Разархивируем в текущую папку
```markdown
unzip "<FILE_NAME>.zip"
```