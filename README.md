# CI/CD Deployment using the CodeCatalyst Invalidate Cloudfront Cache action  
This is a sample create-react-app project that is equipped with a CI/CD workflow 
that automates the build, deployment to an S3 bucket, and invalidation of the CloudFront cache. 
Here's a brief overview of the workflow:

## Build
The source code is built into the build directory using the aws/build@v1.0.0 action. The output artifacts are saved under the name BuildArtifacts.

## Publish to S3
The built application is then published to the gstarkma-react-bucket S3 bucket using the aws/s3-publish@v1.0.5 action.

## Invalidate CloudFront Cache
After deploying to the S3 bucket, the CloudFront cache is invalidated to ensure that users access the updated content from the bucket. This is achieved using the codecatalyst-labs/invalidate-cloudfront-cache@v0.0.1 action.
