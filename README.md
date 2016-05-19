Kafka in Docker
===

This repository provides everything you need to run Kafka in Docker.

Why?
---
The main hurdle of running Kafka in Docker is that it depends on Zookeeper.
Compared to other Kafka docker images, this one runs both Zookeeper and Kafka
in the same container. This means:

* No dependency on an external Zookeeper host, or linking to another container
* Zookeeper and Kafka are configured to work together out of the box

Run
---

Any kafka property can be set by using an env variable prefixed by `_KAFKA_`. All the `.` in the property name have to be replaced by `_` (bash env variables can not contain `.`)

```bash
docker run -p 2181:2181 -p 9092:9092 --env _KAFKA_advertised_host_name=`docker-machine ip \`docker-machine active\`` --env _KAFKA_advertised_port=9092 flozano/kafka
```

```bash
export KAFKA=`docker-machine ip \`docker-machine active\``:9092
kafka-console-producer.sh --broker-list $KAFKA --topic test
```

```bash
export ZOOKEEPER=`docker-machine ip \`docker-machine active\``:2181
kafka-console-consumer.sh --zookeeper $ZOOKEEPER --topic test
```

Public Builds
---

https://registry.hub.docker.com/u/flozano/kafka/


Build from Source
---

    docker build -t flozano/kafka kafka/

Todo
---

* Not particularily optimzed for startup time.
* Better docs

