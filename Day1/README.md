# Day 1: Establishing a Kafka and Zookeeper environment

In this project, we are using Docker Compose to manage our Kafka and Zookeeper services. Docker Compose is a tool that allows us to define and manage multi-container Docker applications. With a single command, we can start, stop, and scale services.

## Zookeeper Service

Zookeeper is a service used by Kafka for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these are used in one form or another by Kafka.

In our docker-compose.yml file, we use the latest Bitnami image for Zookeeper. The environment variable ALLOW_ANONYMOUS_LOGIN is set to yes, which allows us to connect to Zookeeper without any authentication.

## Kafka Service

Our Kafka service also uses the latest Bitnami image. The KAFKA_CFG_ZOOKEEPER_CONNECT environment variable points to our Zookeeper service, allowing Kafka to connect to it. The ALLOW_PLAINTEXT_LISTENER variable is set to yes to allow connections without encryption.

The Kafka service exposes port 9092 for connections from outside of Docker. The depends_on directive specifies that our Kafka service depends on our Zookeeper service.
