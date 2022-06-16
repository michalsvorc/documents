# Processing

## Stream processing vs batch processing

Batch processing:

- Data is collected over time.
- Used when data size is known and finite.
- Once data is collected, it’s sent for processing.
- It processes large volume of data all at once.
- It takes little longer time to processes data.
- Meant for large quantities of information that aren't time-sensitive.

Stream processing:

- Processing of continuous stream of data immediately as it is produced.
- Used when the data size is unknown and infinite and continuous.
- Data is processed piece-by-piece.
- Processing is fast.

## Message queue

- [Wikipedia](https://en.wikipedia.org/wiki/Message_queue)
- [medium.com](https://medium.com/must-know-computer-science/system-design-message-queues-245612428a22)
- [opengenus.org](https://iq.opengenus.org/message-queues/)

A message queue is a form of asynchronous service-to-service communication used in serverless and microservices
architectures. Messages are stored on the queue until they are processed and deleted. Each message is processed only
once, by a single consumer. Message queues can be used to decouple heavyweight processing, to buffer or batch work, and
to smooth spiky workloads.

A message queue provides a lightweight buffer which temporarily stores messages, and endpoints that allow software
components to connect to the queue in order to send and receive messages.

`Producer -> Queue -> Consumer`

Many producers and consumers can use the queue, but each message is processed only once, by a single consumer.

Examples of queues: Kafka, Heron, real-time streaming, Amazon SQS, and RabbitMQ.

Message queue can implement:

- message deduplication
- dead letter queue
- checkpointing: checkpoint for processing based on message offset
- partitioning: multiple queues

## Pub/Sub Messaging

- [Wikipedia](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)
- [amazon.com](https://aws.amazon.com/pub-sub-messaging/)

Publish/subscribe messaging, or pub/sub messaging, is a form of asynchronous service-to-service communication used in
serverless and microservices architectures. In a pub/sub model, any message published to a topic is immediately received
by all of the subscribers to the topic.

Pub/sub messaging can be used to enable event-driven architectures, or to decouple applications in order to increase
performance, reliability and scalability.

A sibling to a message queue, a _message topic_ provides a lightweight mechanism to broadcast asynchronous event
notifications, and endpoints that allow software components to connect to the topic in order to send and receive those
messages.

Unlike message queues, which batch messages until they are retrieved, message topics transfer messages with no or very
little queuing, and push them out immediately to all subscribers.

`Publisher(s) -> Topic -> Suibscriber(s)`

## Message broker

A message broker is an intermediary computer program module that translates a message from the formal messaging protocol
of the sender to the formal messaging protocol of the receiver.

Three standards have emerged which are used in open source message queue implementations:

- Advanced Message Queuing Protocol (AMQP): feature-rich message queue protocol
- Streaming Text Oriented Messaging Protocol (STOMP): simple, text-oriented message protocol
- MQTT (formerly MQ Telemetry Transport): lightweight message queue protocol especially for embedded devices
