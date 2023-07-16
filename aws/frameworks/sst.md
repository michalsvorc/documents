# SST

- https://github.com/serverless-stack/sst/issues
- https://docs.sst.dev/what-is-sst
- https://docs.sst.dev/what-is-sst#project-structure

Builds on top of AWS CDK constructs, provides an escape hatch.

## Auth

- https://docs.sst.dev/auth
- Cognito, Auth0: https://docs.sst.dev/auth#why-not-use-cognito

Supports magic links, OAuth.

## Deploy

- https://docs.sst.dev/advanced/iam-credentials#loading-from-a-file

Only accepts ~/.aws/credentials with secret key?
AWS CDK does not support SSO: https://github.com/serverless-stack/sst/issues/313
