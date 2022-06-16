# AWS CDK

AWS CDK was developed for TypeScript and has a great typing support. This documentation uses AWS CDK v2.

Documentation:

- [API Reference](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-construct-library.html)
- [Additional documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html#additional_docs)

Examples:

- [aws-samples/aws-cdk-examples](https://github.com/aws-samples/aws-cdk-examples/tree/master/typescript)
- [awsdocs/aws-doc-sdk-examples](https://github.com/awsdocs/aws-doc-sdk-examples/tree/master/typescript/example_code)

## Setup

- [AWS CDK Versions](https://docs.aws.amazon.com/cdk/api/versions.html)
- [Prerequisites](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html#getting_started_prerequisites)
- [AWS CDK v2 Prerequisites](https://docs.aws.amazon.com/cdk/latest/guide/work-with-cdk-v2.html#v2-prerequisites)
- [Tools](https://docs.aws.amazon.com/cdk/latest/guide/tools.html)

Although the AWS CDK CLI tool uses credentials from the same configuration files as other AWS tools and SDKs, including
the AWS CLI, it may behave slightly differently from these tools. In particular, if you use a named profile from the
credentials file, the config must have a profile of the same name specifying the region. The AWS CDK does not fall back
to reading the region from the `[default]` section in config.

## Bootstrapping

- [Bootstrapping](https://docs.aws.amazon.com/cdk/latest/guide/bootstrapping.html)
- [Roles](https://docs.aws.amazon.com/cdk/latest/guide/bootstrapping.html#bootstrapping-contract-roles)

AWS environment is a combination of an AWS account and region. Environments are independent, each environment must be
bootstrapped separately.

In AWS CDK v 2, the modern template will be the default [bootstrapping
template](https://docs.aws.amazon.com/cdk/latest/guide/bootstrapping.html#bootstrapping-templates).

The modern bootstrap template effectively grants the permissions implied by the `--cloudformation-execution-policies` to
any AWS account in the `--trust` list, which by default will extend permissions to read and write to any resource in the
bootstrapped account.

It is not an error to bootstrap an environment more than once. If an environment you bootstrap has already been
bootstrapped, its bootstrap stack will be upgraded if necessary; otherwise, nothing happens.

## Overview

- Constructs: Constructs are the basic building blocks of AWS CDK apps. A construct represents a "cloud component" with
  sensible defaults and encapsulates everything AWS CloudFormation needs to create the component.
- Stacks: The unit of deployment. All AWS resources defined within the scope of a stack, either directly or indirectly,
  are provisioned as a single unit. AWS CDK stacks are implemented through AWS CloudFormation stacks.
- Apps: To define the Stack within the scope of an application, use the App construct.

## Identifiers

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/identifiers.html)

Identifiers must be unique within the scope in which they are created; they do not need to be globally unique in your
AWS CDK application.

See also [Physical names](https://docs.aws.amazon.com/cdk/latest/guide/resources.html#resources_physical_names)

## Importing existing external resources

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/resources.html#resources_importing)

You can turn the resource's ARN (or another identifying attribute, or group of attributes) into an AWS CDK object in the
current stack.

## Assets

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/assets.html)

Assets are local files, directories, or Docker images that can be bundled into AWS CDK libraries and apps. Assets can
represent any artifact that the app needs to operate.

By default, the AWS CDK creates a copy of the asset in the [Cloud
assemblies](https://docs.aws.amazon.com/cdk/latest/guide/apps.html#apps_cloud_assembly) directory, which defaults to
cdk.out, under the source hash.

## Environments

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/environments.html)

An environment is the target AWS account and region into which the stack is intended to be deployed.

For all but the simplest deployments, you will need to
[bootstrap](https://docs.aws.amazon.com/cdk/latest/guide/bootstrapping.html) each environment you will deploy into.
Deployment requires certain AWS resources to be available, and these resources are provisioned by bootstrapping.

When using cdk deploy to deploy environment-agnostic stacks, the AWS CDK CLI uses the specified AWS CLI profile (or the
default profile, if none is specified) to determine where to deploy.

Sourced from default profile:

- `process.env.CDK_DEFAULT_ACCOUNT`
- `process.env.CDK_DEFAULT_REGION`

Pass as `env` property to Stack initialization options.

## Permissions

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/permissions.html)

## Runtime context

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/context.html)

Context values are key-value pairs that can be associated with a stack or construct. [Feature
flags](https://docs.aws.amazon.com/cdk/latest/guide/featureflags.html) are also context values.

Context values are made available to your AWS CDK app in six different ways:

- Automatically from the current AWS account.
- Through the --context option to the cdk command.
- In the project's cdk.context.json file.
- In the project's cdk.json file.
- In the context key of your ~/.cdk.json file.
- In your AWS CDK app using the construct.node.setContext method.

## Testing constructs

- [AWS Cloud Development Kit (AWS CDK)](https://docs.aws.amazon.com/cdk/latest/guide/testing.html)

There are three categories of tests you can write for AWS CDK apps:

- Snapshot tests
- Fine-grained assertions
- Validation tests

## CDK Pipelines

Do not delete and recreate an account's bootstrap stack if you are using CDK Pipelines to deploy into that account. The
pipeline will stop working. To update the bootstrap stack to a new version, instead re-run cdk bootstrap to update the
bootstrap stack in place.
