# Static website

- [Use CloudFront to serve a static website hosted on Amazon S3](https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-serve-static-website/)

## www

Just use non-www: [https://moz.com/community/q/topic/65405/should-you-use-www/4](https://moz.com/community/q/topic/65405/should-you-use-www/4)

Select the `CreateApex=yes` option when deploying the template for non-www apex version.

## HTTPS

When you use the Amazon S3 static website endpoint, connections between CloudFront and Amazon S3 are available only over
HTTP. To use HTTPS for connections between CloudFront and Amazon S3, configure an S3 REST API endpoint for your origin.

## Invalidate CloudFront cache and Lambda@Edge functions

```console
aws cloudfront create-invalidation --distribution-id <distribution_ID> --paths "/\*"
```

## Sync S3 bucket

- [Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html#using-s3-commands-managing-objects-sync) with local folder

```console
aws s3 sync <local_dir> <s3://bucket_id> --delete
```

## Amazon CloudFront Secure Static Website

- [Template](https://github.com/aws-samples/amazon-cloudfront-secure-static-site)

### Update Lambda@Edge function

1. Log into the AWS console. Switch to the `us-east-1` region and select `Lambda` service.
2. Open LambdaEdgeFunction associated with your stack.
3. Update the function code in the `Code` tab.
4. Click the `Deploy` button and wait until deployment is finished.
5. Publish a new version in the `Versions` tab. Add an optional description and wait until the new version is published.
6. Leave the versioned function view and return back to the main function view.
7. Click on `Deploy to Lambda@Edge` from the `Actions` dropdown button.
8. Select `Use existing CloudFront trigger on this function` radio button. It should preselect the previous function
   version number with associated CloudFront ID. Click `Deploy`. This action will delete the trigger from the previous
   function version and move it to the newly created function version. You could also do it manually in the `Versions`
   tab.
9. Go to the CloudFront console to monitor distribution status. After the deployment is finished, it can still take a
   while until the new Lambda@Edge version is live.
10. Optional: [Invalidate CloudFront
    cache](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Invalidation.html) immediately, charges
    might apply due to forced replication costs.
