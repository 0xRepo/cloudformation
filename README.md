Extend the provided Cloudformation template to include:
- KMS key
- IAM Role
- IAM managed policy
You do not need to write any lambda function code, but do need to make sure the IAM role allows the lambda function access to only the necessary resources described below.


The `FunctionName` of the lambda function needs to be set to the correct value of "development-example-lambda" or "test-example-lambda" or "production-example-lambda"
Add a tag to the lambda function with a key of "Stack" and a value set to the stack name.
The lambda function needs to know which environment (development/test/production) it is running in. Pass in the value into an environment variable named RUNNING_ENVIRONMENT.


The IAM role will be used the lambda function. The IAM role needs to account for the following:
- The lambda function will output logs which developers will need to see later in Cloudwatch.
- The lambda function needs to be able to create secrets values in AWS Secrets Manager. It should have full access to the secret. However it does not need to read the secret. The names of these secrets must be restricted to start with the environment name, depending on the value passed into the EnvironmentParameter value of the stack.
- The lambda function will encrypt using the KMS key.
- The IAM role's path needs to be passed into the template as a Cloudformation parameter.


The KMS key should have complete access by the AWS account root user.
An existing IAM role, passed into the Cloudformation template in the `AdminRoleNameParameter` parameter should be able to administer the KMS key.
The lambda function will access the KMS key by a friendly name, which should be passed into an environment variable named TEST_KMS_KEY.


An IAM managed policy allowing access to encrypt with the KMS key is required. The managed policy is given to the IAM role.
The ARN of the managed policy needs to be output from the stack for use in other stacks.


