# Terraform

- [Documentation](https://developer.hashicorp.com/terraform)
- [Basic CLI Features](https://developer.hashicorp.com/terraform/cli/commands)

## What is Terraform?

- Terraform is an open-source IaC tool developed by HashiCorp.
- It enables the provisioning and management of infrastructure in a declarative and version-controlled manner.
- Works with multiple cloud providers (AWS, Azure, Google Cloud Platform, etc.) and on-premises environments.

Read more:

- [Terraform](https://www.terraform.io/)
- [HashiCorp](https://www.hashicorp.com/)

## License change

- Previously open-source under the Mozilla Public License v2.0 (open source).
- HashiCorp on 10 August 2023 adopted the Business Source License v1.1 (source available).
- OpenTofu: open source Terraform fork hosted under the Linux Foundation.

Read more:

- [HashiCorp announcement](https://www.hashicorp.com/blog/hashicorp-adopts-business-source-license)
- [Business Source License 1.1](https://mariadb.com/bsl11/)
- [The OpenTofu Manifesto](https://opentofu.org/manifesto/)

## Key Concepts

- Providers: Plugins that define and enable the interaction between Terraform and specific infrastructure platforms through APIs.
- Resources: Fundamental building blocks of infrastructure defined in Terraform configurations, representing specific components.
- Modules: Reusable, self-contained collections of infrastructure configurations that enable modularization and abstraction.

Read more:

- [Terraform registry](https://registry.terraform.io/)
- [Modules](https://developer.hashicorp.com/terraform/language/modules)

Images:

https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-apis.png%26width%3D2048%26height%3D644&w=3840&q=75
https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Drefs%252Fheads%252Fv1.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=3840&q=75

## State file

- Keeps track of the resources that Terraform manages and their current state in the target infrastructure.
- Used by Terraform to to determine which changes to make to your infrastructure..
- Stored by default in a local file named `terraform.tfstate`.
- Can be stored locally or remotely (e.g., S3, Terraform Cloud) to version, encrypt, and securely share it with your team.
- Can contain sensitive information, depending on the resources in use.

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

resource "aws_s3_bucket" "example-bucket" {
  bucket = "my-terraform-bucket"

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
- Allows unit testing of constructs with Jest and dedicated assertions library.

Example:

```typescript
// main.ts
import * as cdk from 'aws-cdk-lib';
import * as s3 from 'aws-cdk-lib/aws-s3';

export class MyStack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    const bucket = new s3.Bucket(this, 'example', {
      bucketName: 'example-bucket',
      versioned: true,
    });
  }
}
```

Read more:

- [AWS CDK](https://docs.aws.amazon.com/cdk/v2/guide/home.html)
- [AWS CDK Examples](https://github.com/aws-samples/aws-cdk-examples)
- [S3 bucket construct](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_s3.Bucket.html)

## Cloud Development Kit for Terraform (CDKTF)

- Access to the entire Terraform ecosystem without learning HashiCorp Configuration Language (HCL).
- Supports multiple languages: TypeScript, Python, Java, C#, and Go.

Example:

```typescript
// main.ts
import { Construct } from "constructs";
import { TerraformStack } from "cdktf";
import { S3Bucket } from "./.gen/providers/aws/s3-bucket";
import { S3BucketVersioningA } from "./.gen/providers/aws/s3-bucket-versioning";

class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);

    const bucket = new S3Bucket(this, "example", {
      bucket: "example-bucket",
    });

    new S3BucketVersioningA(this, "versioning_example", {
      bucket: bucket.id,
      versioningConfiguration: {
        status: "Enabled",
      },
    });
  }
}```

Read more:

- [CDK for Terraform](https://developer.hashicorp.com/terraform/cdktf)
- [S3 bucket construct](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket?lang=typescript)

## CDKTF cons

- CDKTF may still have breaking changes before v1.0 release.
- You cannot yet use AWS CDK constructs within CDKTF. The interoperability layer is a technical preview, and it is not yet ready for use in production.

Read more:

- [AWS Adapter](https://developer.hashicorp.com/terraform/cdktf/create-and-deploy/aws-adapter)

