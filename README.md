# Урок 3 (Развертывание и базовая конфигурация, интерфейсы и инструменты)

# Установка ClickHouse v24.12.3


[docker-compose.yml](docker-compose.yml)

```
services:
  clickhouse-server:
    image: clickhouse/clickhouse-server:24.12.3
    container_name: clickhouse-server
    ulimits:
      nofile:
        soft: 262144
        hard: 262144
    volumes:
      - ./etc/clickhouse-server:/etc/clickhouse-server
      - ./etc/clickhouse-keeper:/etc/clickhouse-keeper
      - ./etc/clickhouse-client:/etc/clickhouse-client
      - ./data:/var/lib/clickhouse
      - ./logs:/var/log/clickhouse-server
    network_mode: host
    cap_add:
      - SYS_NICE
      - NET_ADMIN
      - IPC_LOCK
      - SYS_PTRACE
```

Рабочий инстанс

![1.png](src%2Fimg%2F1.png)

CLI clickhouse-client

![3.png](src%2Fimg%2F3.png)

Для примера создал базу test

``` 
create table test;
use test;
```

Загрузил датасет из объектного хранилища s3

Данные о поездках на такси в Нью-Йорке с 2009 года включают более 3 миллиардов поездок на такси и арендованных автомобилях (Uber, Lyft и т. д.) в Нью-Йорке.

```
CREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetime    DateTime,
    pickup_longitude    Nullable(Float64),
    pickup_latitude     Nullable(Float64),
    dropoff_longitude   Nullable(Float64),
    dropoff_latituCREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetime    DateTime,
    pickup_longitude    Nullable(Float64),
    pickup_latitude     Nullable(Float64),
    dropoff_longitCREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetime    DateTime,
    pickup_longitude    Nullable(Float64),
    pickup_latitudCREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetime    DateTime,
    pickup_longituCREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetiCREATE TABLE trips (
    trip_id             UInt32,
    pickup_datetime     DateTime,
    dropoff_datetime    DateTime,
    pickup_longitude    Nullable(Float64),
    pickup_latitude     Nullable(Float64),
    dropoff_longitude   Nullable(Float64),
    dropoff_latitude    Nullable(Float64),
    passenger_count     UInt8,
    trip_distance       Float32,
    fare_amount         Float32,
    extra               Float32,
    tip_amount          Float32,
    tolls_amount        Float32,
    total_amount        Float32,
    payment_type        Enum('CSH' = 1, 'CRE' = 2, 'NOC' = 3, 'DIS' = 4, 'UNK' = 5),
    pickup_ntaname      LowCardinality(String),
    dropoff_ntaname     LowCardinality(String)
)
ENGINE = MergeTree
PRIMARY KEY (pickup_datetime, dropoff_datetime);

INSERT INTO trips
SELECT
    trip_id,
    pickup_datetime,
    dropoff_datetime,
    pickup_longitude,
    pickup_latitude,
    dropoff_longitude,
    dropoff_latitude,
    passenger_count,
    trip_distance,
    fare_amount,
    extra,
    tip_amount,
    tolls_amount,
    total_amount,
    payment_type,
    pickup_ntaname,
    dropoff_ntaname
FROM s3(
    'https://datasets-documentation.s3.eu-west-3.amazonaws.com/nyc-taxi/trips_{0..2}.gz',
    'TabSeparatedWithNames'
);

```

Тестовый датасет

![4.png](src%2Fimg%2F4.png)

