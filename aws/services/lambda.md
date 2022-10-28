# Lambda

- [Documentation](https://docs.aws.amazon.com/lambda/index.html)
- [Quotas](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html)
- [Best practices](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)

## Resources

- [CLI](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/lambda/index.html)
- [CDK](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_lambda-readme.html)
- [CDK - Node.js](https://docs.aws.amazon.com/cdk/api/v2/docs/aws-cdk-lib.aws_lambda_nodejs-readme.html)
- [Docker image - Node.js](https://hub.docker.com/r/amazon/aws-lambda-nodejs/tags)

## SDK for JavaScript v3

- [client-lambda](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-lambda/index.html)

## Performance

- [Lambda function scaling](https://docs.aws.amazon.com/lambda/latest/dg/invocation-scaling.html)
- [Performance of AWS Lambda with and without
  layers](https://medium.com/consulner/performance-of-aws-lambda-with-and-without-layers-9bffbb5434f3)

## Networking

- [VPC networking for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/foundation-networking.html)
- [Configuring a Lambda function to access resources in a VPC](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html)
- [Configuring interface VPC endpoints for Lambda](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc-endpoints.html)

By default, Lambda runs your functions in a secure VPC. Lambda owns this VPC, which isn't connected to your account's
default VPC. When you connect a function to a VPC in your account, the function can't access the internet unless your
VPC provides access.

To give your function access to the internet, route outbound traffic to a NAT gateway in a public subnet. The NAT
gateway has a public IP address and can connect to the internet through the VPC's internet gateway.

To use your Lambda function with AWS resources in an Amazon VPC, configure it with security groups and subnets to create
a VPC connection. Connecting your function to a VPC lets you access resources in a private subnet such as relational
databases and caches. You can also create a database proxy for MySQL and Aurora DB instances. A database proxy enables a
function to reach high concurrency levels without exhausting database connections.
