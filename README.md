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
Если таблица `order` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.order
PARTITION BY RANGE (YEAR(otus.order.created_at)) (
    PARTITION p0 VALUES LESS THAN (2020),
    PARTITION p1 VALUES LESS THAN (2021),
    PARTITION p2 VALUES LESS THAN (2022),
    PARTITION p3 VALUES LESS THAN (2023),
    PARTITION p4 VALUES LESS THAN (2024),
    PARTITION p5 VALUES LESS THAN MAXVALUE
);
```

Если таблица `review` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.review
   PARTITION BY RANGE (YEAR(otus.review.created_at)) (
      PARTITION p0 VALUES LESS THAN (2020),
      PARTITION p1 VALUES LESS THAN (2021),
      PARTITION p2 VALUES LESS THAN (2022),
      PARTITION p3 VALUES LESS THAN (2023),
      PARTITION p4 VALUES LESS THAN (2024),
      PARTITION p5 VALUES LESS THAN MAXVALUE
);
```

Если таблица `question` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.question
   PARTITION BY RANGE (YEAR(otus.question.created_at)) (
      PARTITION p0 VALUES LESS THAN (2020),
      PARTITION p1 VALUES LESS THAN (2021),
      PARTITION p2 VALUES LESS THAN (2022),
      PARTITION p3 VALUES LESS THAN (2023),
      PARTITION p4 VALUES LESS THAN (2024),
      PARTITION p5 VALUES LESS THAN MAXVALUE
);
```

Если таблица `answer` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.answer
   PARTITION BY RANGE (YEAR(otus.answer.created_at)) (
      PARTITION p0 VALUES LESS THAN (2020),
      PARTITION p1 VALUES LESS THAN (2021),
      PARTITION p2 VALUES LESS THAN (2022),
      PARTITION p3 VALUES LESS THAN (2023),
      PARTITION p4 VALUES LESS THAN (2024),
      PARTITION p5 VALUES LESS THAN MAXVALUE
);
```

Если таблица `shipment` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.shipment
   PARTITION BY RANGE (YEAR(otus.shipment.created_at)) (
      PARTITION p0 VALUES LESS THAN (2020),
      PARTITION p1 VALUES LESS THAN (2021),
      PARTITION p2 VALUES LESS THAN (2022),
      PARTITION p3 VALUES LESS THAN (2023),
      PARTITION p4 VALUES LESS THAN (2024),
      PARTITION p5 VALUES LESS THAN MAXVALUE
);
```


Если таблица `payment` содержит столбец `created_at` с датой создания записей, можно использовать партиционирование по диапазону:

```sql
ALTER TABLE otus.shipment
   PARTITION BY RANGE (YEAR(otus.payment.created_at)) (
      PARTITION p0 VALUES LESS THAN (2020),
      PARTITION p1 VALUES LESS THAN (2021),
      PARTITION p2 VALUES LESS THAN (2022),
      PARTITION p3 VALUES LESS THAN (2023),
      PARTITION p4 VALUES LESS THAN (2024),
      PARTITION p5 VALUES LESS THAN MAXVALUE
);
```