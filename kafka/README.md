
# Kafka and Messaging System Interview Questions

## 1. Kafka Basics and Concepts
- [What is Kafka and how to publish and subscribe messages?](#what-is-kafka-and-how-to-publish-and-subscribe-messages)
- [Why do we need Kafka?](#why-do-we-need-kafka)
- [What is partition and offset in Kafka?](#what-is-partition-and-offset-in-kafka)
- [How Kafka should be configured to consume the same data consumed by multiple systems?](#how-kafka-should-be-configured-to-consume-the-same-data-consumed-by-multiple-systems)
- [How to retrieve messages from Kafka?](#how-to-retrieve-messages-from-kafka)
- [Write implementation of multiple consumers in the same topic in Kafka.](#write-implementation-of-multiple-consumers-in-the-same-topic-in-kafka)
- [How to delete processed messages automatically in Kafka?](#how-to-delete-processed-messages-automatically-in-kafka)
- [How do you debug lag and issues like losing a message in a Kafka topic?](#how-do-you-debug-lag-and-issues-like-losing-a-message-in-a-kafka-topic)
- [Have you used Kafka?](#have-you-used-kafka)
- [Do you have experience with Kafka?](#do-you-have-experience-with-kafka)

## 2. Kafka vs MQ/RabbitMQ
- [Kafka vs MQ message system](#kafka-vs-mq-message-system)
- [Kafka advantages over MQ/RabbitMQ](#kafka-advantages-over-mqrabbitmq)
- [Difference between Topic and Queue?](#difference-between-topic-and-queue)
- [Difference between MQ and Pub-Sub Model](#difference-between-mq-and-pub-sub-model)
- [What is the difference between optimistic locking and pessimistic locking?](#what-is-the-difference-between-optimistic-locking-and-pessimistic-locking)

## 3. Messaging Service Brokers
- [Used any messaging service brokers? ActiveMQ, Kafka?](#used-any-messaging-service-brokers-activemq-kafka)
- [Explain MQ used in your project?](#explain-mq-used-in-your-project)

## 4. Design and Implementation of Notification System
- [Design a notification system (SMS and email) that can handle any kind of notification mechanism and cross-questions on proposed solutions.](#design-a-notification-system-sms-and-email-that-can-handle-any-kind-of-notification-mechanism-and-cross-questions-on-proposed-solutions)
  - [How can we add additional notification mechanisms like WhatsApp?](#how-can-we-add-additional-notification-mechanisms-like-whatsapp)
  - [What happens when a processing thread fails before or after consuming the message?](#what-happens-when-a-processing-thread-fails-before-or-after-consuming-the-message)

## 5. Locking Concepts
- [What is the difference between optimistic locking and pessimistic locking?](#what-is-the-difference-between-optimistic-locking-and-pessimistic-locking)

## 6. Miscellaneous
- [Have you worked on message queues?](#have-you-worked-on-message-queues)

---

## Answer Guide

### What is Kafka and how to publish and subscribe messages?
Kafka is a distributed event streaming platform used for building real-time data pipelines and streaming applications. To publish messages, you use the Kafka producer API, and to consume them, you use the Kafka consumer API.

### Why do we need Kafka?
Kafka is widely used for real-time analytics, log aggregation, and building scalable, fault-tolerant, and low-latency systems. It is also used to decouple microservices by providing a highly reliable event-driven architecture.

### What is partition and offset in Kafka?
A **partition** is a unit of parallelism in Kafka topics. Kafka topics are divided into partitions for scalability. An **offset** is the identifier for each message in a partition. Consumers use offsets to track their position within a partition.

### How Kafka should be configured to consume the same data consumed by multiple systems?
Kafka's consumer groups allow multiple consumers to read from the same topic and consume the same data independently. Each consumer in a group processes different partitions, but for multiple systems to consume the same data, multiple consumer groups can be used.

### How to retrieve messages from Kafka?
Messages can be retrieved from Kafka using the Kafka consumer API. A consumer subscribes to one or more topics, and it starts pulling messages from the topic partitions. Messages are read sequentially, and offsets are tracked for message consumption.

### Write implementation of multiple consumers in the same topic in Kafka.

### How to delete processed messages automatically in Kafka?
Kafka allows you to set a retention policy on topics. Messages will be deleted once they reach the retention time or the log segment size limit is reached. You can configure this with the `log.retention.hours` or `log.retention.bytes` settings.

### How do you debug lag and issues like losing a message in a Kafka topic?
To debug Kafka lag, you can use Kafka's built-in tools such as `kafka-consumer-groups.sh` to monitor consumer lag. If messages are lost, checking broker configurations, replication, and partition settings can help identify the root cause.

### Have you used Kafka?
Yes, I have worked with Kafka in real-time data streaming projects where we use Kafka to connect multiple microservices for real-time event processing.

### Do you have experience with Kafka?
Yes, I have implemented event-driven architectures using Kafka in various applications for high-throughput and low-latency message streaming.

---

