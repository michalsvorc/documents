# AWS CLI

- [Installing or updating the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Credentials

- [Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [Sourcing credentials with an external process](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sourcing-external.html)

## IAM security credentials

- MFA is required only when signing in (web interface?)
- SSH key is used only for for AWS CodeCommit

## s3fs

```console
$ s3fs <bucket_name> <mountpoint_path> -o profile=<aws_profile>
```

Sourcing credentials from an external process does not work.

## Snippets

### Verify current identity

```console
$ aws sts get-caller-identity
```

### ECR

Login:

```console
$ aws ecr get-login-password | docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```

### Lambda functions

Invoke a function:

```console \
$ aws lambda invoke --function-name <function_name> \
--invocation-type RequestResponse \
--cli-binary-format raw-in-base64-out \
--payload '{"key": "value"}' \
response.json
```

### Events

PUT:

```console
$ aws events put-events --entries file://event.json
```

### Expose credentials in current environment

```console
export AWS_ACCESS_KEY_ID=
export AWS_SECRET_ACCESS_KEY=
```
