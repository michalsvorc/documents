# Amazon Simple Queue Service (SQS)

- [Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [API](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/index.html)
- [How Amazon SQS works](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)
- [Queue parameters](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configure-queue-parameters.html)
- [Best parameters](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-best-practices.html)

## Queue types

- [Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html#sqs-queue-types)

### Standard queues

- [Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/standard-queues.html)

Send data between applications when the throughput is important.

- Unlimited Throughput
- At-Least-Once Delivery
- Best-Effort Ordering

### FIFO queues

- [Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html)

Send data between applications when the order of events is important.

- High Throughput (quotas apply)
- Exactly-Once Processing
- First-In-First-Out Delivery
