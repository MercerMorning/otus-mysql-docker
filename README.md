Поднять сервис db_va можно командой:

`docker-compose up otusdb`

Для подключения к БД используйте команду:

`docker-compose exec otusdb mysql -u root -p12345 otus`

Для использования в клиентских приложениях можно использовать команду:

`mysql -u root -p12345 --port=3309 --protocol=tcp otus`

### Партиционирование

#### Обоснование
Партиционирование позволяет разбить большие таблицы на более мелкие, что улучшает производительность запросов и упрощает управление данными.

#### Пример партиционирования по диапазону (Range Partitioning)
Если таблица `product` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.product
PARTITION BY RANGE (YEAR(created_at)) (
    PARTITION p0 VALUES LESS THAN (1991),
    PARTITION p1 VALUES LESS THAN (1995),
    PARTITION p2 VALUES LESS THAN (2000),
    PARTITION p3 VALUES LESS THAN (2005),
    PARTITION p4 VALUES LESS THAN (2010),
    PARTITION p5 VALUES LESS THAN (2015),
    PARTITION p6 VALUES LESS THAN (2020),
    PARTITION p7 VALUES LESS THAN MAXVALUE
);