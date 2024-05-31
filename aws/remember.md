# Remember

## SQS

- [Quotas related to messages](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/quotas-messages.html)
- Always manually delete the message after processing. Helps with batch processing and manually consuming message from DLQ.

## Lambda

- 231115: [Node.js 20.x runtime now available in AWS Lambda](https://aws.amazon.com/blogs/compute/node-js-20-x-runtime-now-available-in-aws-lambda/)
  Changes to Root CA certificate loading: Lambda no longer loads additional CA certificates by default.
