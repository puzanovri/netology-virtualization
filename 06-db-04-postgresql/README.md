# Домашнее задание к занятию "6.4. PostgreSQL"

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 13). Данные БД сохраните в volume.

![1](https://user-images.githubusercontent.com/57503209/185491375-312292a7-6f29-4e3d-ad12-b7d0de82f6a4.jpg)

![2](https://user-images.githubusercontent.com/57503209/185492360-4b758312-1405-4a7b-aec6-daf397d055b0.jpg)

Подключитесь к БД PostgreSQL используя `psql`.

![3](https://user-images.githubusercontent.com/57503209/185491920-47cdf633-835f-4f12-846c-52beb0894d10.jpg)

Воспользуйтесь командой `\?` для вывода подсказки по имеющимся в `psql` управляющим командам.

**Найдите и приведите** управляющие команды для:
- вывода списка БД

![4](https://user-images.githubusercontent.com/57503209/185492086-b1430460-3b5d-4afb-a5e6-7cb8098b2df3.jpg)

- подключения к БД

![5](https://user-images.githubusercontent.com/57503209/185492118-663a05d3-ce36-4a8c-a2b8-30f403dd257c.jpg)

- вывода списка таблиц

![6](https://user-images.githubusercontent.com/57503209/185492214-4cac98ef-add9-44ab-87f6-cdc51d9571fb.jpg)

- вывода описания содержимого таблиц

![7](https://user-images.githubusercontent.com/57503209/185492228-f63c8401-ae26-4e03-8c65-0ac92e36b1fa.jpg)

- выхода из psql

![8](https://user-images.githubusercontent.com/57503209/185492247-3f8d957c-d74f-40da-954f-6c8ab19b24d6.jpg)

## Задача 2

Используя `psql` создайте БД `test_database`.

![21](https://user-images.githubusercontent.com/57503209/185495627-cafbe61c-2225-4f6f-830b-ca40ef040f64.jpg)

Изучите [бэкап БД](https://github.com/netology-code/virt-homeworks/tree/master/06-db-04-postgresql/test_data).

Восстановите бэкап БД в `test_database`.

Перейдите в управляющую консоль `psql` внутри контейнера.

Подключитесь к восстановленной БД и проведите операцию ANALYZE для сбора статистики по таблице.

![22](https://user-images.githubusercontent.com/57503209/185500724-e97aded5-6db0-42a1-9e5c-eda56297b67d.jpg)

Используя таблицу [pg_stats](https://postgrespro.ru/docs/postgresql/12/view-pg-stats), найдите столбец таблицы `orders` 
с наибольшим средним значением размера элементов в байтах.

![23](https://user-images.githubusercontent.com/57503209/185500740-2582e12d-193f-46d7-8347-beaabcf39947.jpg)

**Приведите в ответе** команду, которую вы использовали для вычисления и полученный результат.

## Задача 3

Архитектор и администратор БД выяснили, что ваша таблица orders разрослась до невиданных размеров и
поиск по ней занимает долгое время. Вам, как успешному выпускнику курсов DevOps в нетологии предложили
провести разбиение таблицы на 2 (шардировать на orders_1 - price>499 и orders_2 - price<=499).

Предложите SQL-транзакцию для проведения данной операции.

![31](https://user-images.githubusercontent.com/57503209/185499173-af18dc90-4610-4e12-a76e-0361f2978501.jpg)

Можно ли было изначально исключить "ручное" разбиение при проектировании таблицы orders?

Да.

![32](https://user-images.githubusercontent.com/57503209/185499195-f372579c-6a42-450f-a8b5-203edd7673c8.jpg)

## Задача 4

Используя утилиту `pg_dump` создайте бекап БД `test_database`.

root@d86da0511156:/# export PGPASSWORD=netology && pg_dump -h localhost -U postgres test_database > /tmp/test_database_backup.sql

Как бы вы доработали бэкап-файл, чтобы добавить уникальность значения столбца `title` для таблиц `test_database`?

title character varying(80) NOT NULL UNIQUE,

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
