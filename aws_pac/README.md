# IAM Role and User CloudFormation Template

This CloudFormation template allows you to create an IAM Role with a specified policy and an associated IAM User. The IAM Role provides access to EC2, Elastic Beanstalk, S3, Route 53, and VPC services.

## Parameters

The template includes the following parameters:

- **PolicyName**: (Required) A string that represents the name for the IAM Role policy.
- **UserName**: (Required) A string that represents the name for the IAM User.

## Resources

The template creates the following AWS resources:

### PaCIAMRole

This resource represents the IAM Role that allows access to the specified services.

Properties:

- **RoleName**: The name of the IAM Role. It is derived using the `UserName` parameter.

Policy:

- **AssumeRolePolicyDocument**: The trust policy that defines who can assume the role. It allows the services `ec2.amazonaws.com` and `elasticbeanstalk.amazonaws.com` to assume the role.
- **Policies**: A list of policies associated with the IAM Role. The `PolicyName` property is derived using the `PolicyName` parameter.
  - **PolicyDocument**: The policy document that specifies the permissions for the IAM Role. It allows the following actions on all resources (`Resource: '*'`):
    - `ec2:*`
    - `elasticbeanstalk:*`
    - `s3:*`
    - `route53:*`
    - `vpc:*`

### PaCIAMUser

This resource represents the IAM User.

Properties:

- **UserName**: The name of the IAM User. It is derived using the `UserName` parameter.

### PaCIAMUserAccessKey

This resource represents the access key for the IAM User.

Properties:

- **UserName**: The name of the IAM User.

## Outputs

The template provides the following outputs:

- **IAMRoleARN**: The Amazon Resource Name (ARN) of the IAM Role.
- **IAMUserARN**: The ARN of the IAM User.
- **IAMUserName**: The name of the IAM User.

## Usage

Follow the steps below to use this CloudFormation template:

1. Sign in to the AWS Management Console.
2. Open the CloudFormation service.
3. Create a new stack using this template.
4. Provide values for the `PolicyName` and `UserName` parameters.
5. Review the stack configuration and click "Create Stack".
6. Wait for the stack creation to complete.
7. Retrieve the output values from the CloudFormation stack details or by using the AWS CLI or SDKs.

## Example

Here's an example command using the AWS CLI to create a stack based on this template:

```bash
aws cloudformation create-stack \
    --stack-name IAMRoleUserStack \
    --template-body file://path/to/template.yaml \
    --parameters ParameterKey=PolicyName,ParameterValue=MyPolicy \
                  ParameterKey=UserName,ParameterValue=MyUser
```

Make sure to replace `path/to/template.yaml` with the actual path to the template file.

---