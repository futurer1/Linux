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

### Подготовка запуска кафки из консоли:

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

### Запуск с указанием конфига сервера

Каждый сервер в отдельном терминале.
```
cd kafka_2.13-3.6.1\bin\

./kafka-server-start ..\config\kraft\server-1.properties
```

### Остановка сервера

Ctrl+C - с потерей логов и работы.

Более верно остановить producers и consumers
```
./kafka-server-stop
```

### Управление топиками

Создать новый топик с именем payment-created-events-topic.
Имя должно быть уникальное.

--partitions 3 (кол-во партиций. Кол-во консьюмеров должно быть равно кол-ву партиций для параллельной обработки. Если партиция одна, то все будут ломиться в неё и будет однопоточность.)
--replication-factor 3 (кол-во копий каждой партиции. Одна в лидере и 2 в репликах, не может превышать кол-во серверов)
--bootstrap-server localhost:9092... (список брокеров в кластере. Правильнее перечислить всех)
```
./kafka-topics.sh --create --topic payment-created-events-topic --partitions 3 --replication-factor 3 --bootstrap-server localhost:9092,localhost:9094
```

Получить список всех топиков
```
./kafka-topics.sh --list --bootstrap-server localhost:9092,localhost:9094
```

Более детальная информация про топики
```
./kafka-topics.sh --describe --bootstrap-server localhost:9092,localhost:9094
```

Удаление топика
В конфиге должно быть: delete.topic.enable=true
```
./kafka-topics.sh --delete --topic payment-created-events-topic --bootstrap-server localhost:9092
```
## Работа с сообщениями

Отправка сообщения вручную
В конфиге должно быть (плохая практика!): auto.create.topics.enable=true (для автоматического создания топиков в случае, 
если сообщение пришло в несуществующий топик. Будет предупреждение WARN, то топик создастся.)
```
./kafka-console-producer.sh --bootstrap-server localhost:9092,localhost:9094 --topic payment-cancelled-events-topic --property "parse.key=true" --property "key.separator=:"
```

## Изменение конфига

```
./kafka-configs.sh --bootstrap-server localhost:9092,localhost:9094 --alter --entity-type topics --entity-name tovar-created-events-topic --add-config min.insync.replicas=1
```
