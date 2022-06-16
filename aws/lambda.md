# AWS Lambda

- [Developer guide](https://docs.aws.amazon.com/lambda/latest/dg/index.html)
- [API Reference](https://docs.aws.amazon.com/lambda/latest/dg/API_Reference.html)
- [Operator guide](https://docs.aws.amazon.com/lambda/latest/operatorguide/intro.html)

- [Lambda concepts](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-event)
- [CI](https://docs.aws.amazon.com/lambda/latest/dg/applications-tutorial.html)
- [Lambda resource ARN format](https://docs.aws.amazon.com/lambda/latest/dg/lambda-api-permissions-ref.html)
- [Using AWS Lambda with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html)
- [Monitoring](https://docs.aws.amazon.com/lambda/latest/dg/lambda-monitoring.html)

You can invoke your Lambda functions using the Lambda API, or Lambda can run your functions in response to events from
other AWS services.

You can use runtimes that Lambda provides, or build your own. For a container image, you include the runtime when you
build the image.

The runtime passes in objects to the handler that contain the invocation _event_ and the _context_, such as the function
name and request ID. When the handler finishes processing the first event, the runtime sends it another. The function's
class stays in memory, so clients and variables that are declared outside of the handler method in initialization code
can be reused.

## Pricing

You are charged based on the number of requests for your functions and the duration it takes for your code to execute.

Duration is calculated from the time your code begins executing until it returns or otherwise terminates, rounded up to
the nearest 1 ms. The price depends on the amount of memory you allocate to your function.

## Events

An event is a JSON-formatted document that contains data for a Lambda function to process. The runtime converts the
event to an object and passes it to your function code.

### Event source mappings

- [Lambda event source mappings](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html)

An event source mapping is a Lambda resource that reads from an event source and invokes a Lambda function. You can use
event source mappings to process items from a stream or queue in services that don't invoke Lambda functions directly.

Lambda provides event source mappings for services like DynamoDB. MQ, SQS, Kafka and others.

Event source mappings read items from a stream or queue in batches. Event source mappings include multiple items in the
event that your function receives.

Event source mappings maintain a local queue of unprocessed items and handle retries if the function returns an error or
is throttled. You can configure an event source mapping to customize batching behavior and error handling, or to send a
record of items that fail processing to a destination.

For streams, an event source mapping creates an iterator for each shard in the stream, and processes items in each shard
in order. You can configure the event source mapping to read only new items that appear in the stream, or to start with
older items. Processed items aren't removed from the stream, and other functions or consumers can process them.

By default, if your function returns an error, the entire batch is reprocessed until the function succeeds, or until the
items in the batch expire. To ensure in-order processing, Lambda pauses processing for the affected shard until the
error is resolved.

### Event filtering

- [Lambda event filtering](https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventfiltering.html)

For Amazon SQS and stream event sources, you can also apply filter criteria to incoming events so that you send only
certain events to your Lambda function.

For example, you can define filter criteria so that you process only the records from a Kinesis stream that have the
status code ERROR.

## Lambda layers

- [https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html)
- [Using layers with your Lambda function](https://docs.aws.amazon.com/lambda/latest/dg/invocation-layers.html)

A Lambda layer is a .zip file archive that can contain additional code or other content. A layer can contain libraries,
a custom runtime, data, or configuration files. You can use layers only with Lambda functions deployed as a .zip file
archive.

You can use a layer to distribute a dependency to multiple functions. Functions deployed as a container image do not use
layers.

## Networking

- [VPC networking for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/foundation-networking.html)
- [Configuring a Lambda function to access resources in a VPC](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)
- [Configuring interface VPC endpoints for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc-endpoints.html)

By default, Lambda runs your functions in a secure VPC. Lambda owns this VPC, which isn't connected to your account's
default VPC. When you connect a function to a VPC in your account, the function can't access the internet unless your
VPC provides access.

Lambda accesses resources in your VPC using a Hyperplane ENI.

To give your function access to the internet, route outbound traffic to a NAT gateway in a public subnet. The NAT
gateway has a public IP address and can connect to the internet through the VPC's internet gateway.

To use your Lambda function with AWS resources in an Amazon VPC, configure it with security groups and subnets to create
a VPC connection. Connecting your function to a VPC lets you access resources in a private subnet such as relational
databases and caches. You can also create a database proxy for MySQL and Aurora DB instances. A database proxy enables a
function to reach high concurrency levels without exhausting database connections.

## Lambda extensions

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/using-extensions.html)
- [AWS Lambda Partners](http://aws.amazon.com/lambda/partners/)
- [Create your own Lambda extensions](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-extensions-api.html)

Lambda extensions enable you to augment your functions. For example, you can use extensions to integrate your functions
with your preferred monitoring, observability, security, and governance tools.

## Invocation

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation.html)

When you invoke a function, you can choose to invoke it synchronously or asynchronously.

Lambda invokes your function in an execution environment. The execution environment provides a secure and isolated
runtime environment that manages the resources required to run your function. Lambda re-uses the execution environment
from a previous invocation if one is available, or it can create a new execution environment.

When another AWS service invokes your function, the service chooses the invocation type and retry behavior. AWS services
can invoke your function on a schedule, in response to a lifecycle event on a resource, or to serve a request from a
user. Some services invoke functions asynchronously and let Lambda handle errors, while others retry or pass errors back
to the user.

## Synchronous invocation

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/invocation-sync.html)

When you invoke a function synchronously, Lambda runs the function and waits for a response. When the function
completes, Lambda returns the response from the function's code with additional data, such as the version of the
function that was invoked.

If the function returns an object or error, the response is the object or error in JSON
format. If the function exits without error, the response is `null`.

If Lambda was able to run the function, the status code is `200`, even if the function returned an error.

## Asynchronous invocation

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html)
- [Dead letter queues](https://docs.aws.amazon.com/lambda/latest/dg/invocation-async.html#invocation-dlq)

For asynchronous invocations, Lambda handles retries if the function returns an error or is throttled. To customize this
behavior, you can configure error handling settings on a function.

For asynchronous invocation, Lambda places the event in a queue and returns a success response without additional
information. A separate process reads events from the queue and sends them to your function.

To invoke a function asynchronously, set the invocation type parameter to `Event`.

Lambda manages the function's asynchronous event queue and attempts to retry on errors. If the function returns an
error, Lambda attempts to run it two more times, with a one-minute wait between the first two attempts, and two minutes
between the second and third attempts.

You can also configure Lambda to send an invocation record to another service. Lambda supports the following
destinations for asynchronous invocation. Each destination service requires a different permission.

- Amazon SQS: A standard SQS queue.
  Permission: `sqs:SendMessage`
- Amazon SNS: An SNS topic.
  Permission: `sns:Publish`
- AWS Lambda: A Lambda function.
  Permission: `InvokeFunction`
- Amazon EventBridge: An EventBridge event bus.
  Permission: `events:PutEvents`

Alternatively, you can configure an Amazon SQS queue or Amazon SNS topic as a dead-letter queue for discarded events. To
reprocess events in a dead-letter queue, you can set it as an event source for your Lambda function. If Lambda can't
send a message to the dead-letter queue, it deletes the event and emits the `DeadLetterErrors` metric.

## Permissions

- [AWS Lambda permissions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html)
- [AWS managed policies for Lambda features](https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html#permissions-executionrole-features)

A Lambda function also has a policy, called an execution role, that grants it permission to access AWS services and
resources. At a minimum, your function needs access to Amazon CloudWatch Logs for log streaming.

Use resource-based policies to give other accounts and AWS services permission to use your Lambda resources. Lambda
resources include functions, versions, aliases, and layer versions.

You can use identity-based policies in AWS Identity and Access Management (IAM) to grant users in your account access to
Lambda.

To manage permissions for users and applications in your accounts, use the managed policies that Lambda provides, or
write your own.

### Permissions boundaries for AWS Lambda applications

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/permissions-boundary.html)

When you create an application in the AWS Lambda console, Lambda applies a permissions boundary to the application's IAM
roles. The permissions boundary limits the scope of the execution role that the application's template creates for each
of its functions, and any roles that you add to the template.

The permissions boundary prevents users with write access to the application's Git repository from escalating the
application's permissions beyond the scope of its own resources.

## Lambda function states

- [Guide](https://docs.aws.amazon.com/lambda/latest/dg/functions-states.html)

State provides information about the current status of the function, including whether you can successfully
invoke the function. Function states do not change the behavior of function invocations or how your function runs the
code. Function states include:

- Pending: After Lambda creates the function, it sets the state to pending.
- Active: Your function transitions to active state after Lambda completes resource configuration and provisioning.
  Functions can only be successfully invoked while active.
- Failed: Indicates that resource configuration or provisioning encountered an error.
- Inactive: A function becomes inactive when it has been idle long enough for Lambda to reclaim the external resources
  that were configured for it.

## Performance

- [Lambda function scaling](https://docs.aws.amazon.com/lambda/latest/dg/invocation-scaling.html)
- [Performance of AWS Lambda with and without
  layers](https://medium.com/consulner/performance-of-aws-lambda-with-and-without-layers-9bffbb5434f3)

## Error handling

- [Error handling and automatic retries in AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html)

AWS services can invoke your function synchronously or asynchronously. For synchronous invocation, the service decides
whether to retry. For example, Amazon S3 batch operations retries the operation if the Lambda function returns a
TemporaryFailure response code.

### Invocation errors

Invocation errors occur when the invocation request is rejected before your function receives it. Issues with the
request, caller, or account can cause invocation errors. Invocation errors include an error type and status code in the
response that indicate the cause of the error.

### Function errors

Function errors occur when your function's code or runtime returns an error. Unlike invocation errors, function errors
don't cause Lambda to return a `400`-series or `500`-series status code. If the function returns an error, Lambda
indicates this by including a header named `X-Amz-Function-Error`, and a JSON-formatted response with the error message
and other details.

## Concurrency

- [Quotas](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html)

Concurrency is the number of requests that your function is serving at any given time. When your function is invoked,
Lambda provisions an instance of it to process the event. When the function code finishes running, it can handle another
request. If the function is invoked again while a request is still being processed, another instance is provisioned,
increasing the function's concurrency.

Concurrency is subject to quotas at the AWS Region level. You can configure individual functions to limit their
concurrency, or to enable them to reach a specific level of concurrency.

For an initial burst of traffic, your functions' cumulative concurrency in a Region can reach an initial level of
between 500 and 3000, which varies per Region. Note that the burst concurrency quota is not per-function; it applies to
all your functions in the Region.

As invocations increase exponentially, the function scales up. It initializes a new instance for any request that can't
be routed to an available instance. When the burst concurrency limit is reached, the function starts to scale linearly.
If this isn't enough concurrency to serve all requests, additional requests are throttled and should be retried.

There are two types of concurrency controls available:

- Reserved concurrency
- Provisioned concurrency

### Reserved concurrency

- [Managing Lambda reserved concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html)

Reserved concurrency guarantees the maximum number of concurrent instances for the function. When a function has
reserved concurrency, no other function can use that concurrency. There is no charge for configuring reserved
concurrency for a function.

To prevent a function from using too much concurrency, and to reserve a portion of your account's available concurrency
for a function, use reserved concurrency. Reserved concurrency splits the pool of available concurrency into subsets.

A function with reserved concurrency only uses concurrency from its dedicated pool.

### Provisioned concurrency

- [Managing Lambda provisioned concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html)
- [Predictable start-up times with Provisioned Concurrency](https://aws.amazon.com/blogs/compute/new-for-aws-lambda-predictable-start-up-times-with-provisioned-concurrency/)

When a Lambda function scales out, the process of allocating and initializing new runtime environments may increase
latency for end users. Provisioned Concurrency gives customers more control over cold start performance by enabling them
to create runtime environments in advance.

Provisioned Concurrency runs both environment setup and customer initialization code. This enables runtime environments
to be ready to respond to invocations with low latency and reduces the impact of cold starts for end users.

Note that configuring provisioned concurrency incurs charges to your AWS account.

By allocating provisioned concurrency before an increase in invocations, you can ensure that all requests are served by
initialized instances with low latency. Lambda functions configured with provisioned concurrency run with consistent
start-up latency, making them ideal for building interactive mobile or web backends, latency sensitive microservices,
and synchronously invoked APIs.

## Orchestrating functions with Step functions

- [State machine](https://docs.aws.amazon.com/lambda/latest/dg/lambda-stepfunctions.html)
- [Step functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)

AWS Step Functions is an orchestration service that lets you connect Lambda functions together into serverless
workflows, called state machines.

In Step Functions, you orchestrate your resources using state machines, which are defined using a JSON-based, structured language called Amazon States Language.

The logic of each state determines which state comes next, what data to pass along, and when to terminate the workflow.

You can create complex orchestrations for state machines using application patterns such as:

- Catch and retry: Handle errors using sophisticated catch-and-retry functionality.
- Branching: Design your workflow to choose different branches based on Lambda function output.
- Chaining: Connect functions into a series of steps, with the output of one step providing the input to the next step.
- Parallelism: Run functions in parallel, or use dynamic parallelism to invoke a function for every member of any array.

All work in your Step Functions state machine is done by Tasks. A Task performs work by using an activity, a Lambda
function, or by passing parameters to the API actions of other Supported AWS Service Integrations for Step Functions.

## Best practices

- [Best practices for working with AWS Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)

- Separate the Lambda handler from your core logic.
- Take advantage of execution environment reuse to improve the performance of your function.
- Use a keep-alive directive to maintain persistent connections.
- Use environment variables to pass operational parameters to your function.
- Control the dependencies in your function's deployment package.
- Minimize your deployment package size to its runtime necessities.
- Minimize the complexity of your dependencies.
- Avoid using recursive code in your Lambda function.
