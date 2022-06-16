# Cloud functions

## Python

- [Deploy Python Lambda functions with .zip file archives - AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/python-package.html)

## environment variables

Can be added in the Lambda function dashboard. Secrets Manager service option charges 0.40$ per secret.

## Docker images

- [Creating Lambda container images - AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html)

The container image must be able to run on a read-only file system. Your function code can access a writable /tmp
directory with 512 MB of storage. If you are using an image that requires a writable directory outside of /tmp,
configure it to write to a directory under the /tmp directory.

The default Lambda user must be able to read all the files required to run your function code.

The AWS base images provide the following environment variables:

- `LAMBDA_TASK_ROOT=/var/task`
- `LAMBDA_RUNTIME_DIR=/var/runtime`
