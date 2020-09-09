---
title: "Kafka Introduction"
date: 2020-08-08T23:45:17+02:00
type: 'post'
tags: ["kafka"]
series: ["Kafka"]
---

### Introduction

Kafka is an `event streaming platform`, which provides following functionalities
- `publish` and `subscribe` events
- `store` events indefinitely
- `process` and `analyze` events

## Event
An event has 3 main properties
- key
- value
- timestamp

Each event is a part of a stream, which stores its sequence for [hundreds of years](https://www.confluent.io/blog/publishing-apache-kafka-new-york-times/). They are encoded commonly using AVRO by Kafka Clients

## Streams and KTables

Streams | KTables
:-------|:---------:
Provides immutable Data | Provides mutable data
Supports only inserts for new data | Supports insert, update and delete

Both are concepts of Kafka’s processing layer, which work on "raw" data in topics.


## Kafka Topics

- Sequence of encoded events
- Defines a number of settings like Compression and data retention.
- They can be partitioned across different brokers

## Kafka Brokers

- Machines that actually store and serve the data
- Has no idea about the content of the messages since its encoded.

## Kafka Consumer group
- Bunch of consumers listening to a topic parallely.
- Can rebalance load between consumers within the group, when some of them fails or more are added.
- Operates within a Consumer group protocol

## Kafka Stream Task
- Unit of processing parallelism
- One Stream Task is created for each partition in topic
- Stream task is distributed across app instances




  

Source - 
- https://www.confluent.io/blog/kafka-streams-tables-part-1-event-streaming/
- https://www.confluent.io/blog/kafka-streams-tables-part-2-topics-partitions-and-storage-fundamentals/
- https://www.confluent.io/blog/kafka-streams-tables-part-3-event-processing-fundamentals/