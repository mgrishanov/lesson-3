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