# Step functions

- [Guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [Amazon States Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)

Step Functions gives you several ways to manage your microservice workflows.

States can perform a variety of functions in your state machine:

- Do some work in your state machine (a Task state)
- Make a choice between branches of execution (a Choice state)
- Stop an execution with a failure or success (a Fail or Succeed state)
- Simply pass its input to its output or inject some fixed data (a Pass state)
- Provide a delay for a certain amount of time or until a specified time/date (a Wait state)
- Begin parallel branches of execution (a Parallel state)
- Dynamically iterate steps (a Map state)

## Standard vs. Express Workflows

- [Guide](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-standard-vs-express.html)
- [Execution guarantees](https://docs.aws.amazon.com/step-functions/latest/dg/express-at-least-once-execution.html)

In both cases, you define your state machine using the Amazon States Language. The Type you choose cannot be changed
after your state machine has been created.

### Standard Workflows

- Standard Workflows are ideal for long-running, durable, and auditable workflows.
- Exactly-once workflow execution.
- They can run for up to one year.
- Suited to orchestrating _non-idempotent_ actions, such as starting an Amazon EMR cluster or processing payments.

### Express Workflows

- [Synchronous and Asynchronous Express Workflows](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-express-synchronous.html)

- Express Workflows are ideal for high-volume, event-processing workloads such as IoT data ingestion, streaming data
  processing and transformation, and mobile application backends.
- They can run for up to five minutes.
- Ideal for orchestrating _idempotent_ actions such as transforming input data and storing via PUT in Amazon DynamoDB.
- You should ensure your state machine logic is idempotent and should not be affected adversely by multiple concurrent
  executions of the same input.

#### Asynchronous Express Workflows

- Return confirmation that the workflow was started, but do not wait for the workflow to
  complete.
- At-least-once workflow execution.

#### Synchronous Express Workflows

- Synchronous Express Workflows start a workflow, wait until it completes, then return the result.
- At-most-once workflow execution.

Synchronous Express Workflows can be used to orchestrate microservices, and allow you to develop applications without
the need to develop additional code to handle errors, retries, or execute parallel tasks. Synchronous Express Workflows
can be invoked from Amazon API Gateway, AWS Lambda, or by using the StartSyncExecution API call.
