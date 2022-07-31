# AWS Beanstalk

## Base image

You can use your own base image (e.g. Alpine Linux).

See [Multistage build](https://stackoverflow.com/questions/61518512/aws-elastic-beanstalk-docker-does-not-support-multi-stage-build) issues.

## Use image from ECR

### Setup

Policy for Beanstalk to read ECR:

1. open [https://console.aws.amazon.com/iam/home#roles](https://console.aws.amazon.com/iam/home#roles)
2. Choose aws-elasticbeanstalk-ec2-role
3. On the Permissions tab, choose Attach policies.
4. select AmazonEC2ContainerRegistryReadOnly
5. Choose Attach policy

Documentation:

- [Docker images](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.container.console.html#docker-images)
- [Building custom images with a Dockerfile](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/single-container-docker-configuration.html#docker-configuration.no-compose)

### Config file

1. Upload `Docker.run.json` when creating a new application.
2. Application Code > Upload your code.
3. Source code origin > Local file.

Upload:

```json
{
  "AWSEBDockerrunVersion": "1",
  "Image": {
    "Name": "<ID>.dkr.ecr.us-east-1.amazonaws.com/<IMAGE>:<TAG>",
    "Update": "true"
  },
  "Ports": [
    {
      "ContainerPort": "8080"
    }
  ]
}
```

This config file is saved to Beanstalk S3 bucket.

## Environment variables

You should be able to specify sensitive values as environment variables from eb web console:

Your EB app -> Your EB environment -> Configuration -> Software Configuration -> Environment Properties

Alternatively, you can make use of [eb setenv](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-setenv.html).
