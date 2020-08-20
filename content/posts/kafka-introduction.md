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

Each event is a part of a stream, which stores its sequence for [hundreds of years](https://www.confluent.io/blog/publishing-apache-kafka-new-york-times/)

## Streams and KTables

Streams | KTables
:-------|:---------:
Provides immutable Data | Provides mutable data
Supports only inserts for new data | Supports insert, update and delete


## Kafka Topics

- Sequence of encoded events
- Defines a number of settings like Compression and data retention.
- Events are encoded in commonly using AVRO by Kafka Clients
- They can be partitioned across different brokers

## Kafka Brokers

- Machines that actually store and serve the data
- No idea about the content of the messages since its encoded.


  

Source - 
- https://www.confluent.io/blog/kafka-streams-tables-part-1-event-streaming/
- https://www.confluent.io/blog/kafka-streams-tables-part-2-topics-partitions-and-storage-fundamentals/?