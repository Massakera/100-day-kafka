# Day 3: Kafka consumers

Today, we focus on creating a Kafka consumer. This consumer will be integrated with the producer from Day 2 to complete the process of message exchange between the producer and consumer.

The consumer will connect to a Kafka broker, listen to the topic "myTopic", and consume any messages produced to this topic.

## We initiate a new Kafka consumer with some necessary configurations:

- bootstrap.servers points to the Kafka broker.
- group.id defines the consumer group.
- auto.offset.reset is set to "earliest" to consume messages from the start of the topic.

### Message Consumption Loop

 The consumer continuously listens for new messages using a for loop. When a message arrives:

- It prints the topic and partition info along with the message value.
- If there's an error while reading a message, it prints the error and breaks out of the loop.

### Graceful Shutdown

After the loop breaks (due to an error or manual interruption), the consumer closes its connection to free up resources.

## Usage

1. Make sure your Kafka broker is running and accessible at localhost:29092.

1. Run the consumer:

```bash
go run consumer.go
```

## To read about: Kakfa consumers

A consumer is a component or service designed to receive and process messages. In Kafka, a consumer reads records (messages) from one or many Kafka topics.

Key Aspects of a Kafka Consumer:

- **Consumer Groups**: Multiple consumers can form a consumer group, where each consumer reads from a distinct partition of a topic, enabling parallel processing. Each message in a topic is delivered to one consumer instance within a consumer group.
- **Offsets**: Each record in a Kafka partition has a unique sequence ID known as an offset. Consumers use this offset to track their progress. For example, if a consumer processes a message with an offset of 5, it knows it should process the message with an offset of 6 next.
- **Fault-tolerance**: Consumers keep track of their offset position, and in case of failures, they can pick up right where they left off. Kafka itself can store these offsets, or they can be managed by the consumer itself.
- **Pull Model**: Kafka consumers pull messages from topics. This is in contrast to many other messaging systems where messages are pushed to consumers. This pull model gives consumers control over the rate at which they process messages.

## How the prouducer and the consumer works together?

- **Producers** send records to Kafka topics. These records are stored across various partitions and replicated across multiple brokers for fault-tolerance.
- **Consumers** then subscribe to these topics and start pulling records for processing. If a topic has multiple partitions, and there's a consumer group with multiple consumer instances, the load of processing messages from these partitions is distributed among these consumers.
- As consumers process these messages, they keep updating their offset, ensuring that every record is processed once and only once (at least in an ideal scenario without failures).
- The cycle continues with producers sending more records and consumers processing them, enabling a real-time or near-real-time data processing pipeline.