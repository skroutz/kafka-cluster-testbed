# Kafka Cluster Testbed

A Kafka cluster testbed for testing & development.

Services
--------

- Zookeeper (3 nodes)
- Kafka (2 nodes)
- Rafka (1 node)

Dependencies
------------

- `docker.io`
- `docker-compose`
- `libnss-docker` (optional)
- `kafkacat` (optional, for testing)

Usage
-----

```shell
# Prepare cluster
$ docker-compose build
$ docker-compose up (Ctrl-C to stop)

# Create a new topic
$ docker-compose exec kc1.docker /opt/bitnami/kafka/bin/kafka-topics.sh --bootstrap-server kc1:9092 --topic top1 --partitions 2 --replication-factor 2 --create
top1
$ docker-compose exec kc1.docker /opt/bitnami/kafka/bin/kafka-topics.sh --describe
Topic:top1	PartitionCount:2	ReplicationFactor:2	Configs:
	Topic: top1	Partition: 0	Leader: 1	Replicas: 1,2	Isr: 1,2
	Topic: top1	Partition: 1	Leader: 2	Replicas: 2,1	Isr: 2,1

# Pub/Sub
$ echo "Hello Kafka" | kcat -P -b kc1.docker -t top1
$ kcat -C -b kc1.docker -t top1 -c 1
Hello Kafka

# Rafka
$ redis-cli -p 6380 rpushx topics:top1 "hello there"

# Remove everything
$ docker-compose down
```
