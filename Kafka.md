### Настройка конфигурации

Номер ноды, идентификатор сервера в кластере.
```
node.id=1
```

Список адресов host:port для брокеров и контроллеров. Внутренние адреса.
```
listeners=PLAINTEXT://:9096,CONTROLLER://:9097
```

Список голосующих, принимающих решение по обеспечению согласованности данных и отказоустойчивости. Управляет лидерами (leader) и фолловерами (follower)
```
controller.quorum.votes=1@localhost:9093,2@localhost:9095,3@localhost:9097
# id ноды @ хост:порт
```

Адреса для соединения с брокером для прослушивания входящих соединений. Указывается только брокер.
Если брокер отделен прокси-сервером, то могут быть указаны внешние адреса.
```
advertised.listeners=PLAINTEXT://localhost:9096
```

Локальная папка для хранения метаданных, логов, snapshots. Для каждого сервера индивидуально.
```
log.dirs=/tmp/server-1/kraft-combined-logs
```

Подготовка запуска кафки из консоли:
```
# заходим в папку кластера
cd \bin

# генерим id для кластера
./kafka-storage random-uuid
ak284hka82kfh8329hfhak

# форматнем директорию для очистки данных для каждого сервера
./kafka-storage format -t ak284hka82kfh8329hfhak -c ..\config\kraft\server-1.properties
Formatting /tmp/server-1/kraft-combined-logs with metadata.version 3.6-IV2.

./kafka-storage format -t ak284hka82kfh8329hfhak -c ..\config\kraft\server-2.properties
Formatting /tmp/server-2/kraft-combined-logs with metadata.version 3.6-IV2.

./kafka-storage format -t ak284hka82kfh8329hfhak -c ..\config\kraft\server-3.properties
Formatting /tmp/server-3/kraft-combined-logs with metadata.version 3.6-IV2.
```
