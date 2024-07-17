# AWS CLI

- [CLI reference](https://docs.aws.amazon.com/cli/latest/reference/index.html)
- [Installing or updating the latest version of the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

## Authentication

- [Authentication and access credentials](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html)

### AWS IAM Identity Center (SSO)

- [Configure SSO](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html)

To configure both an IAM Identity Center profile and sso-session to your AWS CLI, follow the [CLI guide](https://docs.aws.amazon.com/cli/latest/userguide/sso-configure-profile-token.html#sso-configure-profile-token-auto-sso).

You can add `--no-browser` to prevent opening a web browser.

If you specify default as the profile name, this profile becomes the one used whenever you run an AWS CLI command and do not specify a profile name.

Q: Allow botocore-client-* to access your data?
A: The sign in process may prompt you to allow the AWS CLI access to your data. Since the AWS CLI is built on top of the SDK for Python, permission messages may contain variations of the botocore name.

### Verify current identity

```shell
aws sts get-caller-identity
```

---

## Credentials

- [Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [Sourcing credentials with an external process](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sourcing-external.html)

## IAM security credentials

- MFA is required only when signing in (web interface?)
- SSH key is used only for for AWS CodeCommit

## s3fs

```shell
s3fs <bucket_name> <mountpoint_path> -o profile=<aws_profile>
```

Sourcing credentials from an external process does not work.

## Snippets

### ECR

Login:

```shell
aws ecr get-login-password | docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```

### Lambda functions

Invoke a function:

```shell \
aws lambda invoke --function-name <function_name> \
--invocation-type RequestResponse \
--cli-binary-format raw-in-base64-out \
--payload '{"key": "value"}' \
response.json
```

### Events

PUT:

```shell
aws events put-events --entries file://event.json
```

### Expose credentials in current environment

```shell
export AWS_ACCESS_KEY_ID=
export AWS_SECRET_ACCESS_KEY=
```
