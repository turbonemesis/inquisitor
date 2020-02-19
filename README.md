# Serverless Inquisitor

A simple app for testing request latency over API Gateway and Lambda functions.

## Prerequisites

* npm
* jekyll
* make

## Usage

1. deploy the stack using `make deploy`


Here are the parameters you can pass to it. All parameters are optional:

* `STACK_NAME`: name of the stack; default is sls-inquisitor-test
* `DEPLOYMENT_BUCKET`: name of the bucket for cloudformation packaging; the bucket will be created if it does not exist; the default name is based on the stack name and deployment region
* `AWS_REGION`: the region where to deploy
* `AWS_PROFILE`: the AWS cli profile to use for deployment
* `PROVISIONED_INSTANCES`: the number of Lambda instances to set up as provisioned concurrency for the testing function. By default, no instances are provisioned. **AWS Charges you for provisioned instances even when you are not using them, so make sure to undeploy stacks with provisioned instances when done with testing**
* `MEMORY_SIZE`: Memory size allocated to the testing lambda function

for example:

```
make deploy STACK_NAME=perf-test AWS_PROFILE=claudia-test AWS_REGION=eu-west-2 PROVISIONED_INSTANCES=5
```

2. start the local web site based on the deployed stack

```
make web STACK_NAME=perf-test
```

## Clean up

You can delete temporarily generated files using `make clean`;

You can remove the deployed stack using `make undeploy` (make sure to add `STACK_NAME`, `AWS_PROFILE` and `AWS_REGION` if you used those arguments during deployment)

## Customising

* modify [sync-test-function/lambda.js](sync-test-function/lambda.js) to change the Lambda function source code 
* modify [template.yml](template.yml) to change the Lambda function settings

