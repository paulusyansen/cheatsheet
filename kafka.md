### Kafka start zookeeper & kafka server
```sh
$ ./zookeeper-server-start.sh ../config/zookeeper.properties
$ ./kafka-server-start.sh ../config/server.properties
$ ./kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic kafka-event
```

### Kafka reassign partition
```sh
{"version":1,
  "partitions":[
     {"topic":"signals","partition":0,"replicas":[0,1,2]},
     {"topic":"signals","partition":1,"replicas":[0,1,2]},
     {"topic":"signals","partition":2,"replicas":[0,1,2]}
]}

$ kafka-reassign-partitions --zookeeper localhost:2181 --reassignment-json-file increase-replication-factor.json --execute
```

### Kafka producer consumer
```sh
$ kafka-console-producer.sh --broker-list localhost:9092 --topic test
$ kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic my-replicated-topic
```

### Kafka describe topics
```sh
$ kafka-topics.sh --describe --zookeeper localhost:2181 --topic my-replicated-topic
```

### Kafka checking end offset
```sh
$ kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group event-agg --describe
```
