# Команды консоли PSQL
----
``` bash
\с "имя базы данных без кавычек"- подключиться к базе данных
\q - выйти
\l - (л) вывести список баз данных
\dn - вывести список схем
\dn+ - вывести список схем с доп. инфо
\dt - вывести список таблиц
\dt 'имя схемы без кавычек'.* - вывести все таблицы из схемы
\dnS - вывести список схем вместе со скрытыми(служебными) схемами
\set ECHO_HIDDEN on/off - показать/скрыть выполняемые запросы командой
\conninfo - информация по подключению к БД
\db - посмотреть табличные пространства
\! sudo mkdir /var/lib/postgresql/"имя_директории" - создание новой директории путь_директории/имя_директории
\! sudo chown "имя_пользователя" /"путь_директории"/"имя_директории" - смена владельца каталога.

```

## Запросы к базам
----
``` bash
SELECT pg_current_wal_lsn() - посмотреть позицию записи в журнале предзаписи.
SELECT * FROM pg_ls_waldir() - открыть журнал предзаписи в PSQL
ALTER TABLE 'имя таблицы' SET SCHEMA 'имя схемы' - перенести таблицу в указанную схему 
SELECT current_schemas(false/true) - вывести (доступные/и системные) схемы
SET search_path = схема1, схема"- установить пути поиска на уровне сеанса
ALTER DATABASE 'имя_бд' SET seatch_path = 'имя_схемы1','имя_схемы_n' - установить путь поиска на уровне ДБ
SHOW - показать
SHOW shared_biffers - показать размер буферного кеша.
SELECT datname FROM pg_database - вывести существующие базы данных
SELECT nspname FROM pg_namespace - вывести схемы в таблице
SELECT relname, relkind, relnamespace FROM pg_class WHERE relname = 'имя_таблицы' - вывести имя таблицы, тип объекта, схему в  таблице указанной в WHERE. relnamespace - oid
SELECT relname, relkind, relnamespase::regnamespace::text FROM pg_class WHERE relname = 'имя_таблицы' - тоже, что и выше, только вместо oid будет имя схемы.
SELECT relname FROM pg_class WHERE relnamespace = 'pg_catalog'::regnamespace - список объектов в схеме pg_catalog.
DROP SCHEMA 'имя' CASCADE - удаление схемы со всеми объектами. Без CASCADE требуется сначала удаление объектов.
DROP DATABASE 'имя_дб' WITH (FORCE) - удаление бд с принудительным отключением всех подключений.
CREATE TABLESPASE "имя_табличного_пространства" LOCATION 'путь_директории' - создание табличного пространства.
CREATE DATABASE 'имя_бд'TABLESPACE 'имя_тп'- создание бд в указанном табличном пространстве
SELECT pg_relation_filepath('имя_таблицы') - расположение файлов, из которых состоит объект

```

### Размеры
----
``` bash
SELECT pg_database_size('имя_бд') - узнать размер бд.
SELECT pg_size_pretty(pg_database_size('имя_бд')) - узнать размер бд в МБ
SELECT pg_size_pretty(pg_total_relation_size('имя_таблицы')) - узнать размер вместе с индексами
SELECT pg_size_pretty(pg_table_size('имя_таблицы')) - узнать размер таблицы
SELECT pg_size_prerry(pg_indexes_size('имя_таблицы')) - размер индексов
SELECT pg_size_pretty(pg_relation_size('имя_таблицы','main')) - узнать размер основного слоя ('fsm'/'vm')
SELECT pg_size_pretty(pg_tablespace_size('имя_тп') - размер табличного пространства

```

# Команды консоли UNIX
----

## общие команды
Ниже ссылка на справочник от edu.postgrespro.ru
[Краткий справочник команд Unix](https://edu.postgrespro.ru/16/dev1-16/unix_commands.pdf)

``` bash
pg_ctlcluster "имя_кластера без кавычек" restart - перезапуск сервера
pg_ctlcluster stop -m immediate - моментальная остановка сервера
sudo bash -c 'cd /var/lib/posgtresql/16/main/"инфо из pg_relation_filepath кроме последнего числа"; ls -l "последнее число"*' - файлы и их слои
sudo rm -rf "путь" - удалить директорию

```