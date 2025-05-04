```
bin/kafka-topics.sh --help
```
![[Screenshot 2024-09-05 at 6.15.34 PM 1.png]]


Topics are Like Kafka's NotePad Where Kafka stores the events or messages.

Kafka Producers writes to Kafka Topics and Topics are consumed by Kafka Consumer.
- Each Producer can write to one or multiple Topic

### Partitions & replication

Kafka is a fault-tolerant system, meaning that if a system within a cluster goes offline, the others can provide the data. For each Kafka cluster, there is a replication factor. The replication factor minus 1 equals the number of system failures the cluster can withstand without losing any data. The maximum replication factor is equal to the number of the servers in the cluster. The fault-tolerance is handled by replicating topic partitions within the cluster.

List of Topics available
```shell
bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```

- kafka-console-producer
- Kafka Connect
- APIs

Optional Prams
```shell
--from-beginning
--max-message
```

```shell
kafka-console-consumer  --bootstrap-server localhost:9092 --topic phishing-sites --from-beginning --max-messages 3
```

```shell

kafka-topics --bootstrap-server localhost:9092 --topic testing_with_rep2 --create --replication-factor 2 --partition 2
```

```shell
kafka-topics --bootstrap-server localhost:9092 --topic testing --describe
```

#### **What is Zookeeper?**

Zookeeper is a **distributed coordination service** used by Apache Kafka (and other distributed systems) to manage metadata, configurations, and leader election.

---

#### **Why Does Kafka Need Zookeeper?**

Before Kafka 2.8, **Zookeeper was required** for Kafka to function. It helped Kafka in:

1. **Broker Management**
    - Tracks which Kafka brokers (nodes) are alive.
2. **Leader Election**
    - Elects a leader for each partition (important for fault tolerance).
3. **Topic & Partition Metadata**
    - Stores topic configurations and partition details.
4. **Consumer Group Coordination**
    - Helps consumers track which messages they’ve read.


## What is ZooKeeper?

Our first question is, what is ZooKeeper? ZooKeeper is a software framework for managing information and providing services necessary for running distributed systems. We'll discuss some of those tasks more in a moment. ZooKeeper is primarily used by developers to create distributed applications, but users do interact with it to manage those applications. A few examples of applications using ZooKeeper include Kafka, the distributed processing framework Hadoop, and the graph database Neo4j.

## 3. What does ZooKeeper do?

Let's talk for a moment about what ZooKeeper actually does. It provides the various services necessary to run distributed applications. This includes handling any configuration information and the naming of systems to prevent conflicts. It also provides the ability to synchronize across systems, such as determining what systems are available, when they should start, how services can reach them, and so forth. ZooKeeper also provides any other basic service that would be required for a group of systems to communicate. It's important to note that ZooKeeper is designed as a framework so that each individual distributed application is not required to implement a custom version of these services. As an example, think about how a power plug or water hose nozzle implements common standards vs each having its own. This allows for easier configuration, implementation, and interaction.


