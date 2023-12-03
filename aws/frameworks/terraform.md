# Terraform

- [Documentation](https://developer.hashicorp.com/terraform)
- [Basic CLI Features](https://developer.hashicorp.com/terraform/cli/commands)

AWS:

- [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Tutorials](https://developer.hashicorp.com/terraform/tutorials/aws?utm_offer=ARTICLE_PAGE&utm_content=DOCS&utm_source=WEBSITE&utm_medium=WEB_IO)

Tools:

- [Terraform version manager](https://github.com/tfutils/tfenv)

## AWS example

- [Basic tutorial](https://developer.hashicorp.com/terraform/tutorials/cdktf/cdktf-build?variants=cdk-language%3Atypescript)

### Post init

- Add provider dependencies: `cdktf provider add "aws@~>4.0"` || `npm install @cdktf/provider-aws`
- Setup [eslint](https://typescript-eslint.io/getting-started)

### HCL -> CDKTF

```shell
cat main.tf | cdktf convert --provider "aws@~>4.0"  > main.ts
```

Try
https://developer.hashicorp.com/terraform/cdktf/cli-reference/commands#convert
https://developer.hashicorp.com/terraform/tutorials/aws/lambda-api-gateway

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

### AWS SAM local invocation

- [Overview](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html)
- [Testing and debugging](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-test-and-debug.html)

Terraform support:

- [AWS SAM support for HashiCorp Terraform now generally available](https://aws.amazon.com/blogs/compute/aws-sam-support-for-hashicorp-terraform-now-generally-available/)
- [Better together: AWS SAM CLI and HashiCorp Terraform](https://aws.amazon.com/blogs/compute/better-together-aws-sam-cli-and-hashicorp-terraform/)

Resources support:

- API Gateway v1 and v2
- Lambda functions
- DynamoDB

CDKTF support:

- Reads HCL: Any Terraform or AWS SAM command must run from the location of the main.tf file.

Notes:

- Hot reloading? []

### LocalStack

- [Overview](https://www.localstack.cloud/)

Resources support:

- [List](https://docs.localstack.cloud/user-guide/aws/feature-coverage/)
- API Gateway v2 only in PRO version

CDKTF support:

https://docs.localstack.cloud/user-guide/integrations/cdk-for-terraform/

Notes:

- Uses serverless framework behind the scenes.
- Hot reloading? []

---

# Presentation

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

- [Terraform APIs](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-apis.png%26width%3D2048%26height%3D644&w=3840&q=75)
- [Terraform workflow](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=3840&q=75)

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

resource "aws_s3_bucket" "example-id" {
  bucket = "example-bucket-name"

  versioning {
    enabled = true
  }
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
import * as s3 from "aws-cdk-lib/aws-s3";

export class MyStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const bucket = new s3.Bucket(this, "example-id", {
      bucketName: "example-bucket-name",
      versioned: true,
    });
  }
}
```

Images:

- [AWS CDK application architecture](https://docs.aws.amazon.com/images/cdk/v2/guide/images/AppStacks.png)

Read more:

- [AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/home.html)
- [AWS CDK Examples](https://github.com/aws-samples/aws-cdk-examples)
- [S3 bucket construct](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_s3.Bucket.html)
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
import { TerraformStack } from "cdktf";
import { S3Bucket } from "./.gen/providers/aws/s3-bucket";
import { S3BucketVersioningA } from "./.gen/providers/aws/s3-bucket-versioning";

class MyStack extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);

    const bucket = new S3Bucket(this, "example-id", {
      bucket: "example-bucket-name",
    });

    new S3BucketVersioningA(this, "bucket-versioning-example", {
      bucket: bucket.id,
      versioningConfiguration: {
        status: "Enabled",
      },
    });
  }
}
```

Images:

- [CDKTF application architecture](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform-cdk%26version%3Dv0.19.1%26asset%3Dwebsite%252Fdocs%252Fcdktf%252Fconcepts%252Fimages%252Fcdktf-app-architecture.png%26width%3D4096%26height%3D3066&w=3840&q=75)
- [CDKTF workflow](https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform-cdk%26version%3Dv0.19.1%26asset%3Dwebsite%252Fdocs%252Fcdktf%252Fconcepts%252Fimages%252Fcdktf-terraform-workflow.png%26width%3D4096%26height%3D3070&w=3840&q=75)

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
