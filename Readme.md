# Команды консоли PSQL
----
``` bash
SHOW - показать
SHOW shared_biffers - показать размер буферного кеша.
\с "имя базы данных без кавычек"- подключиться к базе данных
\q - выйти
SELECT pg_current_wal_lsn() - посмотреть позицию записи в журнале предзаписи.
SELECT * FROM pg_ls_waldir() - открыть журнал предзаписи в PSQL

```

# Команды консоли UNIX
----

## общие команды
Ниже ссылка на справочник от edu.postgrespro.ru
[Краткий справочник команд Unix](https://edu.postgrespro.ru/16/dev1-16/unix_commands.pdf)

``` bash
pg_ctlcluster "имя_кластера без кавычек" restart - перезапуск сервера
pg_ctlcluster stop -m immediate - моментальная остановка сервера


```