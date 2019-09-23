# .NET Lambda GitHub Actions
This .NET Lambda GitHub Actions repository provides an action that uses the AWS .NET Lambda tools to package and upload a .NET package to a Lambda function.

## Getting Started

Create a GitHub Action workflow in a private repository hosting a .NET project with the following code in a workflow:

```
name: Deploy to dev environment
on:
  push:
    branches:
      - develop
jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1

    - name: Use .NET 2.1
      uses: actions/setup-dotnet@v1
      with:
        dotnet-version: 2.1.500

    - name: Use AWS CLI
      uses: actions/aws/cli@master

    - name: .NET Lambda build and deploy
      uses: evalytica/dotnet-lambda-actions/deploy@v0.1.0
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        AWS_REGION: us-east-1
        DOTNET_LAMBDA_PACKAGE_NAME: latest.zip
        DOTNET_LAMBDA_FUNCTION_HANDLER: Host::MyLambdaDomain.Host.LambdaEntryPoint::FunctionHandlerAsync
        DOTNET_LAMBDA_FUNCTION_NAME: my-lambda-function-name
        DOTNET_LAMBDA_S3_LOCATION: my-lambda-builds-bucket/my-lambda-function-name
        DOTNET_LAMBDA_WORKING_DIR: ./src
```

## Actions

### Deploy Action

Given:

* `DOTNET_LAMBDA_WORKING_DIR`: .NET project directory
* `AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`: AWS credentials
* `AWS_REGION`: AWS region *(default: us-east-1)*
* `DOTNET_LAMBDA_PACKAGE_NAME`: Filename to use for zipped package archive. *(default: latest.zip)*
* `DOTNET_LAMBDA_S3_LOCATION`: S3 bucket/key to upload package archive to *(example: <bucket_name>/<key/folder>)*
* `DOTNET_LAMBDA_FUNCTION_NAME`: Lambda function name
* `DOTNET_LAMBDA_FUNCTION_HANDLER`: Lambda function handler

This action will package the project, update the Lambda function with the packaged code, and deploy the function.
