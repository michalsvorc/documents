# Terraform

- [Documentation](https://developer.hashicorp.com/terraform)
- [Basic CLI Features](https://developer.hashicorp.com/terraform/cli/commands)

Notes:

AWS:

- [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Tutorials](https://developer.hashicorp.com/terraform/tutorials/aws?utm_offer=ARTICLE_PAGE&utm_content=DOCS&utm_source=WEBSITE&utm_medium=WEB_IO)

Tools:

- [Terraform version manager](https://github.com/tfutils/tfenv)

AWS example:

- [Basic tutorial](https://developer.hashicorp.com/terraform/tutorials/cdktf/cdktf-build?variants=cdk-language%3Atypescript)

Post init:

- Add provider dependencies: `cdktf provider add "aws@~>4.0"` || `npm install @cdktf/provider-aws`
- Setup [eslint](https://typescript-eslint.io/getting-started)

HCL -> CDKTF

```shell
cat main.tf | cdktf convert --provider "aws@~>4.0"  > main.ts
```

## What is Terraform?

- Terraform is an open-source IaC tool developed by HashiCorp.
- HashiCorp is a software company with a freemium business model based in San Francisco, California.
- Terraform enables the provisioning and management of infrastructure in a declarative and version-controlled manner.
- Works with multiple cloud providers (AWS, Azure, Google Cloud Platform, etc.) and on-premises environments. (Note: Akamai, New Relic)

Read more:

- [Terraform](https://www.terraform.io/)
- [HashiCorp](https://www.hashicorp.com/)
- [List of providers](https://registry.terraform.io/browse/providers)

## License change

- Previously open-source under the Mozilla Public License 2.0 (open source).
- On 10 August 2023 HashiCorp adopted the Business Source License 1.1 (source available).
- OpenTofu: open source Terraform fork hosted under the Linux Foundation.

Read more:

- [HashiCorp announcement](https://www.hashicorp.com/blog/hashicorp-adopts-business-source-license)
- [The OpenTofu Manifesto](https://opentofu.org/manifesto/)
- [Implications and Reactions](https://www.hekto.co/skorfmann/hashicorp-license-change)
- [Mozilla Public License 2.0](https://www.mozilla.org/en-US/MPL/2.0/)
- [Business Source License 1.1](https://mariadb.com/bsl11/)

## Key Concepts

- Providers: Plugins that define and enable the interaction between Terraform and specific infrastructure platforms through APIs.
- Resources: Fundamental building blocks of infrastructure defined in Terraform configurations, representing specific infrastructure components.
- Modules: Reusable, self-contained collections of infrastructure configurations that enable modularization and abstraction.

Images:

<img title="Terraform APIs" src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-apis.png%26width%3D2048%26height%3D644&w=3840&q=75" width="860" style="display: block;" />
<img title="Terraform workflow" src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=3840&q=75" width="860" style="display: block;" />

Read more:

- [Providers](https://developer.hashicorp.com/terraform/language/providers)
- [Resources](https://developer.hashicorp.com/terraform/language/resources)
- [Modules](https://developer.hashicorp.com/terraform/language/modules)
- [Terraform registry](https://registry.terraform.io/)

## State file

- Keeps track of the resources that Terraform manages and their current state in the target infrastructure.
- Used by Terraform to determine which changes to make to your infrastructure.
- Stored by default in a local file named `terraform.tfstate`.
- Can be stored locally or remotely (e.g., S3, Terraform Cloud) to version, encrypt, leverage lock mechanism and securely share it with your team.
- Can contain sensitive information, depending on the resources in use. (Terraform Cloud, HashiCorp Vault, S3 encrypt at rest)
- Comparable to CloudFormation Stack.

Read more:

- [State](https://developer.hashicorp.com/terraform/language/state)

## Terraform language

- Terraform configurations are written in HashiCorp Configuration Language (HCL).
- Configuration files are written with the extension `.tf`.

Example:

```hcl
# main.tf

provider "aws" {
  region = "us-east-1"
}

resource "aws_lambda_function" "example-lambda" {
  function_name = "example-lambda-function"
  filename      = "path/to/lambda_function.zip"
  handler       = "index.handler"
  runtime       = "nodejs18.x"
}
```

Read more:

- [Terraform Language Documentation](https://developer.hashicorp.com/terraform/language)

## AWS Cloud Development Kit (CDK)

- Open-source IaC framework using familiar programming languages.
- Supports multiple languages: TypeScript, Python, Java, C#, and Go.
- Infrastructure components are abstracted as constructs, reusable building blocks that encapsulate AWS resources.
- Translates CDK configurations to AWS CloudFormation templates.
- Benefits: access to types, unit tests with familiar test frameworks.

Example:

```typescript
// main.ts
import * as cdk from "aws-cdk-lib";
import * as lambda from "aws-cdk-lib/aws-lambda";

export class MyStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const lambdaFn = new lambda.Function(this, "example-lambda", {
      functionName: "example-lambda-function",
      runtime: lambda.Runtime.NODEJS_18_X,
      handler: "index.handler",
      code: lambda.Code.fromAsset("path/to/lambda_function.zip"),
    });
  }
}
```

Images:

<img title="AWS CDK application architecture" src="https://docs.aws.amazon.com/images/cdk/v2/guide/images/AppStacks.png"
width="860" style="display: block;" />

Read more:

- [AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/home.html)
- [AWS CDK Examples](https://github.com/aws-samples/aws-cdk-examples)
- [Lambda function construct](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_lambda.Function.html)
- [Test assertions](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.assertions-readme.html)

## Cloud Development Kit for Terraform (CDKTF)

- Access to the entire Terraform ecosystem without learning HashiCorp Configuration Language (HCL).
- Supports multiple languages: TypeScript, Python, Java, C#, and Go.
- Can translate existing HCL into a preferred CDKTF language.
- CDKTF applications are interoperable with Terraform projects written in HCL.
- Translates CDKTF configurations to JSON configuration files for Terraform.
- CDKTF may still have breaking changes before v1.0 release (currently v0.19.1).

Example:

```typescript
// main.ts
import { Construct } from "constructs";
import { TerraformStack, TerraformAsset, AssetType } from "cdktf";
import { lambdaFunction } from "@cdktf/provider-aws";

class MyStack extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);

    const asset = new TerraformAsset(this, "lambda-asset", {
      path: "path/to/lambda_function.zip",
      type: AssetType.ARCHIVE,
    });

    const lambdaFn = new lambdaFunction.LambdaFunction(this, "example-lambda-function", {
      functionName: "example-lambda-function",
      handler: "index.handler",
      runtime: "nodejs18.x",
      filename: "lambda_function_payload.zip",
    });
  }
}
```

Images:

<img title="CDKTF application architecture" src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform-cdk%26version%3Dv0.19.1%26asset%3Dwebsite%252Fdocs%252Fcdktf%252Fconcepts%252Fimages%252Fcdktf-app-architecture.png%26width%3D4096%26height%3D3066&w=3840&q=75" width="860" style="display: block;" />
<img title="CDKTF workflow" src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform-cdk%26version%3Dv0.19.1%26asset%3Dwebsite%252Fdocs%252Fcdktf%252Fconcepts%252Fimages%252Fcdktf-terraform-workflow.png%26width%3D4096%26height%3D3070&w=3840&q=75" width="860" style="display: block;" />

Read more:

- [CDK for Terraform](https://developer.hashicorp.com/terraform/cdktf)
- [S3 bucket resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket?lang=typescript)
- [Lambda function resource](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lambda_function?lang=typescript)
- [CDKTF milestones](https://github.com/hashicorp/terraform-cdk/milestones)

## CDKTF relation to AWS CDK

- CDKTF uses the AWS CDK, which provides a set of language-native frameworks for defining infrastructure,
  and adapters that let underlying provisioning tools use those definitions.
- AWS CDK constructs cannot yet be used within CDKTF.
  The AWS Adapter (interoperability layer) is a technical preview and not ready for production usage.

Read more:

- [AWS Adapter](https://developer.hashicorp.com/terraform/cdktf/create-and-deploy/aws-adapter)

## Local development

Required:

- The Terraform CLI (1.2+)
- Node.js v16+, npm
- CDKTF CLI

Optional:

- [TF env](https://github.com/tfutils/tfenv)

Read more:

- [Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [CDKTF CLI](https://developer.hashicorp.com/terraform/tutorials/cdktf/cdktf-install#install-cdktf)

### AWS SAM

CDKTF support:

- [AWS SAM support for HashiCorp Terraform now generally available](https://aws.amazon.com/blogs/compute/aws-sam-support-for-hashicorp-terraform-now-generally-available/)
- [Better together: AWS SAM CLI and HashiCorp Terraform](https://aws.amazon.com/blogs/compute/better-together-aws-sam-cli-and-hashicorp-terraform/)
- Reads HCL: Any Terraform or AWS SAM command must run from the location of the main.tf file.

#### Local invocation

- [Overview](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html)
- [Testing and debugging](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-test-and-debug.html)

Resources support:

- API Gateway v1 and v2
- Lambda functions
- DynamoDB

#### AWS SAM Accelerate

- [Overview](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/using-sam-cli-sync.html)
- [Blogpost](https://aws.amazon.com/blogs/compute/accelerating-serverless-development-with-aws-sam-accelerate/)

The `--code` flag works only for services:

- AWS::Serverless::Function
- AWS::Lambda::Function
- AWS::Serverless::LayerVersion
- AWS::Lambda::LayerVersion
- AWS::Serverless::Api
- AWS::ApiGateway::RestApi
- AWS::Serverless::HttpApi
- AWS::ApiGatewayV2::Api
- AWS::Serverless::StateMachine
- AWS::StepFunctions::StateMachine

### LocalStack

- [Overview](https://www.localstack.cloud/)

Resources support:

- [List](https://docs.localstack.cloud/user-guide/aws/feature-coverage/)
- PRO version:
  - API Gateway v2
  - Authorizers
  - AppConfig
  - AppSync
  - CloudFront
  - Cognito Identity & Provider
  - DocumentDB
  - Elastic Container Services & Registry
  - Relational Database Service (RDS) / Aurora Serverless

CDKTF support:

- [Integration guide](https://docs.localstack.cloud/user-guide/integrations/cdk-for-terraform/)

Read more:

- [Hot reloading](https://docs.localstack.cloud/user-guide/tools/lambda-tools/hot-reloading/)
- [awslocal cli](https://docs.localstack.cloud/user-guide/integrations/aws-cli/#localstack-aws-cli-awslocal)

Notes:

- [Test project](https://github.com/hashicorp/learn-cdktf-assets-stacks-lambda), refactored to REST API Gateway to use
  comunity edition.

```shell
localstack start
cdktf synth && cdktf deploy [app] [--auto-approve]
```

Interact with REST API GW:

```shell
awslocal apigateway get-rest-apis
curl -X GET http://localhost:4566/restapis/<api_id>/<stage>/_user_request_/<endpoint>/
```

Lambda logs:

```shell
awslocal lambda list-functions
awslocal logs tail /aws/lambda/<lambda_name>
```
