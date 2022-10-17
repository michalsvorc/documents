# Serverless framework

- [Guide](https://www.serverless.com/framework/docs/providers/aws/guide/deploying)
- [Serverless.yml](https://www.serverless.com/framework/docs/providers/aws/guide/serverless.yml)
- [Serverless CLI](https://www.serverless.com/framework/docs/providers/aws/cli-reference)
- [Workflow tips](https://www.serverless.com/framework/docs/providers/aws/guide/workflow)

## Plugins

- [Plugins](https://www.serverless.com/plugins)
- [Lift](https://github.com/getlift/lift): Expanding Serverless Framework beyond functions using the AWS CDK.

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

## Events

- [Ref](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-ref.html)
- [GetAtt](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-getatt.html)

Infrastructure which is created to support events in the events list may be referenced using CloudFormation intrinsic
functions like `Fn::GetAtt` or `Fn::Ref` (or their shorthand counterparts).

### API Gateway

API Gateway comes in two versions:

- v1, also called `REST API`
- v2, also called `HTTP API`, which is faster and cheaper than v1

Read the full comparison in the [AWS
documentation](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html).

The default and maximal API Gateway timeout is used: 30s.

## IAM function permissions

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/iam)

AWS Lambda functions need permissions to interact with other AWS services and resources in your account. These
permissions are set via an AWS IAM Role, which the Serverless Framework automatically creates for each service, and is
shared by all functions in the service.

By default, one IAM Role is shared by all the Lambda functions in your service. Also by default, your Lambda functions
have permission to create and write to CloudWatch logs. 

You can also create function-specific roles to customize permissions per function.

## Parameters

- [Documentation](https://www.serverless.com/framework/docs/guides/parameters)

Parameters can be defined in serverless.yml, Serverless Dashboard or passed via CLI with `--param="<key>=<value>"` flag. 

Parameters can then be used via the `${param:XXX}` variables.

### Stage parameters

Parameters can be defined for each stage in serverless.yml under the `params` key. Use the `default` key to define
parameters that apply to all stages by default.

## Variables

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/variables)
- [dotenv support](https://www.serverless.com/framework/docs/environment-variables)

To use variables, you will need to reference values enclosed in `${}` brackets.

```yaml
# serverless.yml file
yamlKeyXYZ: ${variableSource}

# this is an example of providing a default value as the second parameter
otherYamlKey: ${variableSource, defaultValue}
```

### CLI options ${opt:}

To reference CLI options that you passed, use the `${opt:<option>}` syntax in your serverless.yml configuration file.

### Properties in serverless.yml ${self:}

To self-reference properties in serverless.yml, use the ${self:someProperty} syntax in your serverless.yml. someProperty
can contain the empty string for a top-level self-reference or a dotted attribute reference to any depth of attribute.

### Serverless core variables ${sls:}

Serverless initializes core variables which are used internally by the Framework itself. Those values are exposed via
the Serverless Variables system and can be re-used with the {sls:} variable prefix.

The `${sls:stage}` variable is a shortcut for `${opt:stage, self:provider.stage, "dev"}`.

### Environment variables ${env:}

To reference environment variables, use the ${env:SOME_VAR} syntax in your serverless.yml configuration file.

Keep in mind that sensitive information which is provided through environment variables can be written into less
protected or publicly accessible build logs, CloudFormation templates, et cetera.

### CloudFormation outputs ${cf:}

You can reference CloudFormation stack output values as the source of your variables to use in your service with the
`cf:stackName.outputKey` syntax.

### S3 objects ${s3:}

You can reference S3 values as the source of your variables to use in your service with the `s3:bucketName/key` syntax.

### SSM Parameter Store ${ssm:}

You can reference SSM Parameters as the source of your variables with the `ssm:/path/to/param` syntax.

### AWS-specific variables ${aws:}

You can reference AWS-specific values as the source of your variables. Those values are exposed via the Serverless
Variables system through the {aws:} variable prefix.


The region used by the Serverless CLI. The `${aws:region}` variable is a shortcut for `${opt:region,
self:provider.region, "us-east-1"}`.

### AWS Secrets Manager ${ssm:}

Variables in AWS Secrets Manager can be referenced using SSM, just use the
`ssm:/aws/reference/secretsmanager/secret_ID_in_Secrets_Manager syntax`.

### Reference properties in other files ${file():}

You can reference properties in other YAML or JSON files.

To reference properties in other JSON files use the ${file(./myFile.json):someProperty} syntax. It is important that the
file you are referencing has the correct suffix, or file extension, for its file type (.yml for YAML or .json for JSON)
in order for it to be interpreted correctly.

You can reference JavaScript modules to add dynamic data into your variables. 

To rely on exported someModule property in myFile.js you'd use the following code `${file(./myFile.js):someModule}`.

### Read string variable values as boolean values

To ensure a boolean value is returned, read the string variable value as a boolean value.

Example: `${strToBool(${ssm:API_GW_DEBUG_ENABLED})}`

## Resources

- [Documentation](https://www.serverless.com/framework/docs/providers/aws/guide/resources)

All Resources are other AWS infrastructure resources which the AWS Lambda functions in your Service depend on, like AWS
DynamoDB or AWS S3.

What goes into `resources` property is raw CloudFormation template syntax in YAML.

Every stage you deploy to with serverless.yml using the aws provider is a single AWS CloudFormation stack.

You can override the specific CloudFormation resource to apply your own options (place all such extensions at
resources.extensions section). Extending using resources.extensions only works on the Resources part of the
CloudFormation template.
