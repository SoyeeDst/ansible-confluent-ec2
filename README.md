# Confluent streaming platform

Ansible role to install and configure [Confluent streaming platform][1] on RHEL / CentOS 6.

[Confluent streaming platform][1] is a streaming platform utilizing Kafka as the basic message bus. It improves Apache Kafka by expanding its integration capabilities, adding tools to optimize and manage Kafka clusters, and methods to ensure the streams are secure. Confluent Platform makes Kafka easier to build and easier to operate. 

## Requirements

Platform: RHEL / CentOS 6

Java: Oracle JDK 8

The Oracle Java 8 JDK role from Ansible Galaxy can be used if one is needed.

`$ ansible-galaxy install sleighzy.java-8`

#### Important facts

| Item | Value |
|------|-------------|
| confluent_major_version | 3.3 |
| confluent_scala_version | 2.11 (the exect reason requiring JDK 8) |
| user | confluent |
| user group | confluent | 

#### Ports

| Port | Description |
|------|-------------|
| 9092 | Kafka listener port |
| 2181 | ZooKeeper service port |
| 2888 | ZooKeeper master slave heartbeaten port |
| 3888 | ZooKeeper leader election port | 
| 8081 | Schema registry service port | 
| 8082 | Rest proxy service port |


#### Key Directories and Files

| Directory / File | |
|-----|----|
| Kafka installation directory (symlink to installed version) | `/etc/kafka` |
| Kafka configuration file | `/etc/kafka/server.properties` |
| Directory to store data files | `/var/lib/kafka/logs` |

#### Service init files

| Service name | location |
|--------------|----------|
| ZooKeeper service | `/etc/init.d/zookeeper` |
| Kafka service | `/etc/init.d/kakfa` |
| Schema registry | `/etc/init.d/schemaregistry` | 
| Rest proxy | `/etc/init.d/restproxy` |
| Kafka connect | `/etc/init.d/connect` |

All the services are installed on runlevel 345 by default, updating the template to meet your own.

## Steps to restart service
* service zookeeper start
* service kafka start
* service schemaregistry start
* service restproxy start
* service connect start

Attempts to reverse above actions to stop service gracefully

[1]: https://www.confluent.io/
