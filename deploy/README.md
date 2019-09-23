# DotNet Lambda Deploy Actions

Given:

* `DOTNET_LAMBDA_WORKING_DIR`: .NET project directory
* `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`: AWS credentials
* `AWS_REGION`: AWS region *(default: us-east-1)*
* `DOTNET_LAMBDA_PACKAGE_NAME`: Filename to use for zipped package archive. *(default: latest.zip)*
* `DOTNET_LAMBDA_S3_LOCATION`: S3 bucket/key to upload package archive to *(example: <bucket_name>/<key/folder>)*
* `DOTNET_LAMBDA_FUNCTION_NAME`: Lambda function name
* `DOTNET_LAMBDA_FUNCTION_HANDLER`: Lambda function handler

This action will package the project, update the Lambda function with the packaged code, and deploy the function.
