# Serverless framework

- [Guide](https://www.serverless.com/framework/docs/providers/aws/guide/deploying)
- [Serverless.yml](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml)
- [Serverless CLI](https://www.serverless.com/framework/docs/providers/aws/cli-reference)

## Functions

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/functions)

### VPC configration

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/functions#vpc-configuration)
- [VPC networking for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/foundation-networking.html)

A Lambda function always runs inside a VPC owned by the Lambda service. Lambda owns this VPC, which isn't connected to
your account's default VPC. Lambda applies network access and security rules to this VPC and Lambda maintains and
monitors the VPC automatically. If your Lambda function needs to access the resources in your account VPC, configure the
function to access the VPC.

You can add VPC configuration to a specific function in serverless.yml by adding a vpc object property in the function
configuration.

By default, when a Lambda function is executed inside a VPC, it loses internet access and some resources inside AWS may
become unavailable. In order for S3 resources and DynamoDB resources to be available for your Lambda function running
inside the VPC, a VPC end point needs to be created. 

### Versioning

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/functions#versioning-deployed-functions)
- [Lambda function versions](https://docs.aws.amazon.com/lambda/latest/dg/configuration-versions.html)

By default, the framework creates function versions for every deploy. This behavior is optional, and can be turned off
in cases where you don't invoke past versions by their qualifier.