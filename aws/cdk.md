# AWS CDK

Documentation:

- [Developer Guide](https://docs.aws.amazon.com/cdk/v2/guide/home.html)
- [API Reference](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-construct-library.html)

Resources:

- [Additional resources](https://docs.aws.amazon.com/cdk/latest/guide/home.html#additional_docs)
- [kalaiser/awesome-cdk](https://github.com/kalaiser/awesome-cdk#static-websites)
- [Construct Hub](https://constructs.dev/search?q=&cdk=aws-cdk&cdkver=2&offset=0)
- [CDK Patterns](https://cdkpatterns.com/)
- [AWS Solutions Constructs](https://docs.aws.amazon.com/solutions/latest/constructs/welcome.html)

Blogs:

- [AWS Developer Tools Blog](https://aws.amazon.com/blogs/developer/category/developer-tools/aws-cloud-development-kit/)
- [CDK Resources | Posts](https://cdk.dev/posts)

Examples:

- [aws-samples/aws-cdk-examples](https://github.com/aws-samples/aws-cdk-examples/tree/master/typescript)
- [awsdocs/aws-doc-sdk-examples](https://github.com/awsdocs/aws-doc-sdk-examples/tree/master/typescript/example_code)

## Setup

- [Documentation](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html)
- [Tools](https://docs.aws.amazon.com/cdk/latest/guide/tools.html)
- [AWS CDK Versions](https://docs.aws.amazon.com/cdk/api/versions.html)
- [Supported languages](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html#getting_started_languages)

### Bootstrapping

- [Bootstrapping](https://docs.aws.amazon.com/cdk/latest/guide/bootstrapping.html)
- [CLI Bootstrap](https://docs.aws.amazon.com/cdk/v2/guide/cli.html#cli-bootstrap)
- [Environments](https://docs.aws.amazon.com/cdk/v2/guide/environments.html)

Deploying stacks with the AWS CDK requires dedicated Amazon S3 buckets and other containers to be available to AWS CloudFormation during deployment.

Bootstrapping is the process of provisioning resources for the AWS CDK before you can deploy AWS CDK apps into an AWS environment. 
An AWS environment is a combination of an AWS account and Region. Environments are independent.

It is not an error to bootstrap an environment more than once. If an environment you bootstrap has already been
bootstrapped, its bootstrap stack will be upgraded if necessary; otherwise, nothing happens.

## Overview

- Constructs: Constructs are the basic building blocks of AWS CDK apps. A construct represents a "cloud component" with
  sensible defaults and encapsulates everything AWS CloudFormation needs to create the component.
- Stacks: The unit of deployment. All AWS resources defined within the scope of a stack, either directly or indirectly,
  are provisioned as a single unit. AWS CDK stacks are implemented through AWS CloudFormation stacks.
- Apps: To define the Stack within the scope of an application, use the App construct.

## Constructs

- [Documentation](https://docs.aws.amazon.com/cdk/v2/guide/constructs.html)

The main CDK package is called `aws-cdk-lib`, and it contains the majority of the AWS Construct Library.
It also contains base classes like Stack and App that are used in most CDK applications.

The `constructs` package contains the Construct base class. It's in its own package because it's used by other construct-based tools in addition to the AWS CDK, including CDK for Terraform and CDK for Kubernetes.

### Layers

- [Documentation](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html#getting_started_concepts)

Layer 1: AWS CloudFormation-only

- automatically generated from the AWS CloudFormation specification
- AWS CloudFormation resources always have names that begin with `Cfn`
- all L1 resources are in aws-cdk-lib

Layer 2: Curated

- developed by the AWS CDK team to address specific use cases and simplify infrastructure development
- for the most part, they encapsulate L1 resources, providing sensible defaults and best practice security policies
- aws-cdk-lib contains L2 constructs that are designated stable

Layer 3: Patterns

- declare multiple resources to create entire AWS architectures for particular use cases

## Identifiers

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/identifiers.html)

Identifiers must be unique within the scope in which they are created; they do not need to be globally unique in your
AWS CDK application.

See also [Physical names](https://docs.aws.amazon.com/cdk/latest/guide/resources.html#resources_physical_names)

## Importing existing external resources

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/resources.html#resources_importing)

You can turn the resource's ARN (or another identifying attribute, or group of attributes) into an AWS CDK object in the
current stack.

## Assets

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/assets.html)

Assets are local files, directories, or Docker images that can be bundled into AWS CDK libraries and apps. Assets can
represent any artifact that the app needs to operate.

By default, the AWS CDK creates a copy of the asset in the [Cloud
assemblies](https://docs.aws.amazon.com/cdk/latest/guide/apps.html#apps_cloud_assembly) directory, which defaults to
cdk.out, under the source hash.

## Environments

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/environments.html)

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

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/permissions.html)

## Runtime context

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/context.html)

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

- [Documentation](https://docs.aws.amazon.com/cdk/latest/guide/testing.html)

There are three categories of tests you can write for AWS CDK apps:

- Snapshot tests
- Fine-grained assertions
- Validation tests

## CDK Pipelines

Do not delete and recreate an account's bootstrap stack if you are using CDK Pipelines to deploy into that account. The
pipeline will stop working. To update the bootstrap stack to a new version, instead re-run cdk bootstrap to update the
bootstrap stack in place.
