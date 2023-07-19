# Day 2: Kafka Producers and Topics using Go

Today, we will be diving into two fundamental components of Kafka - Producers and Topics. A Kafka producer is an entity that publishes data into Kafka, and a topic is a category or feed name where records are published.

In essence, producers send records to topics. These records, once published, should be written to a log in a topic for consumption. The records sent by the producer are then appended to the partition in a topic.

In Kafka, a topic is split into one or more partitions, and the producer decides which partition to send each message to. This allows for the workload to be distributed across different systems and for multiple consumers to read from a topic in parallel.

We will write a simple Go program that connects to a Kafka server running on your local machine (or Docker container), sends a series of messages to a specified topic, and reports back whether these messages have been successfully published.

## Instructions

First, ensure that you have a Kafka server running and accessible from your Go environment.

Next, install the Kafka client library for Go using the following command in your terminal:

```bash
go get -u github.com/confluentinc/confluent-kafka-go/kafka
```

Then, refer to the provided Go program in `producer.go` file which connects to a Kafka instance and sends messages to a topic. This program includes:

- Connection to a local Kafka instance
- A loop to send a series of words as separate messages
- A goroutine to monitor the delivery reports of produced messages
- A flush command to ensure all messages are delivered before the program exits
- You can run the program using the following command in your terminal:

```bash
go run producer.go
```

### Short explanation about producer.go

- We create a new Kafka producer that connects to Kafka running on localhost.
- We create a goroutine to monitor the delivery reports of produced messages.
- We send a series of words as separate messages to the "myTopic" Kafka topic.
- We wait for up to 15 seconds for any undelivered messages to be delivered before we exit.

You can replace "localhost" with the address of your Kafka instance if it's not running locally.

Remember, you'll need to have a Kafka instance running and accessible from your Go application. If you're using Docker, ensure that the Kafka container is running and that your Go application can connect to it.
