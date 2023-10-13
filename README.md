# CI/CD Deployment with CodeCatalyst's Cloudfront Cache Invalidation

This repository showcases the application of the `InvalidateAmazonCloudFrontCache` action from CodeCatalyst, as defined in `.codecatalyst/workflows/InvalidateCloudfrontCacheSampleWorkflow.yml`.

While designed for integration within an Amazon CodeCatalyst workspace, full 
utilization requires a setup based on an accompanying tutorial or the blog post
linked with this repository. For more information, refer to the **Resources** section.

At its heart, this repository centers on a `create-react-app` project, 
seamlessly integrated with a CI/CD workflow. This workflow, detailed in 
`.codecatalyst/workflows/InvalidateCloudfrontCacheSampleWorkflow.yml`, streamlines the process of building the app, deploying it to an S3 bucket, and ensuring the CloudFront cache is invalidated. The beauty lies in the simplicity: by just configuring the action and its parameters within `.codecatalyst/workflows/InvalidateCloudfrontCacheSampleWorkflow.yml`, the entire automation process is set in motion. Here's a closer look at the primary stages of the workflow:

## Build
By harnessing the `aws/build@v1.0.0` action, the source code is processed using 
the standard `create-react-app build` recommendations, specifically through 
`npm install` and `npm run build`. This yields the HTML and JavaScript contents 
found in the `build/**/*` directories. The `Build` action configuration can be
left as is. 

## Publish to S3
Upon completion of the build process, the output stored in the `build/**/*` directories is transferred to the specified `DestinationBucket` S3 bucket using the `aws/s3-publish@v1.0.5 action`. It's imperative to update `DevelopmentEnvironment`, `DevelopmentConnection`, `CodeCatalystWorkflowDevelopmentRole`, and `DestinationBucket` to align with your configurations in CodeCatalyst and your AWS account. For comprehensive guidance, refer to the **Resources** section.

## Invalidate CloudFront Cache
Before proceeding, ensure that the S3 bucket, to which you've deployed, is 
configured as a CloudFront origin domain. For guidance on this setup, refer to 
the **Resources** section.

Once your S3 bucket is appropriately configured, it's essential to invalidate 
the Cloudfront cache post-deployment. This ensures end-users consistently 
access the most recent content. The `codecatalyst-labs/invalidate-cloudfront-cache@v0.0.1` action efficiently manages this operation, assuming your S3 bucket functions as an origin in your Cloudfront configuration.

## Resources
[Setting up CodeCatalyst](https://docs.aws.amazon.com/codecatalyst/latest/userguide/setting-up-topnode.html)
[Adding the "Amazon S3 publish" action](https://docs.aws.amazon.com/codecatalyst/latest/userguide/s3-pub-action.html)
[Getting started with a simple CloudFront distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.SimpleDistribution.html)

## Security
For security-related details, kindly refer to [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications).

## License
This library abides by the MIT-0 License. For comprehensive details, please refer to the LICENSE file.
