# Events

## Read

- [AWS Event-Driven Architecture](https://aws.amazon.com/event-driven-architecture/)
- [Event-Driven with Lambda](https://event-driven-architecture.workshop.aws/3-lambda.html)

## Remember

When the event bridge name (ARN) is not specified during the put event, rules at `default` bridge will receive the event. To use custom bridges, you need to specify the custom bridge name.

## AWS Events - Amazon EventBridge

- [Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/aws-events.html)

detail: A JSON object, whose content is at the discretion of the service originating the event.

## Content-based Filtering with Event Patterns - Amazon EventBridge

- [Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/content-filtering-with-event-patterns.html)

With event pattern content filtering you can write complex rules that only trigger under very specific conditions. For instance, you might want a rule that will trigger only when a field of the event is within a specific numeric range.

## Amazon EventBridge | Event Bus | Amazon Web Services

- [Documentation](https://aws.amazon.com/eventbridge/)

### Creating an EventBridge Rule That Triggers on an AWS API Call Using AWS CloudTrail

- [Documentation](https://docs.aws.amazon.com/eventbridge/latest/userguide/create-eventbridge-cloudtrail-rule.html)

To create a rule that triggers on an action by an AWS service that does not emit events, you can base the rule on API calls made by that service.

If you configure CloudTrail to track API calls in multiple Regions and you want a rule based on CloudTrail to trigger in each of those Regions, you must create a separate rule in each Region that you want to track.

## CRON

- [Schedule Expressions for Rules - Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html)
- [The cron Expression for Monitoring Schedule - Amazon SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/model-monitor-schedule-expression.html)

AWS cron seems to have a different format than POSIX.

6 spaces instead of 5, starting from 1 instead of 0, usage of ?, …

## Lambda

Lambda asynchronous invocations can put an event or message on Amazon Simple Notification Service (SNS), Amazon Simple
Queue Service (SQS), or Amazon EventBridge for further processing.

### Invocation

- [Asynchronous invocation - AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html)

`--invocation-type Event`
