# nodejs-terraform

## Login to AWS with access key and secret

Create an AWS IAM user with CLI and AdministratorAccess rights.

Copy the access key and secret to GitHub at:
Secrets and variables -> Actions -> Repository secrets

AWS_ACCESS_KEY_ID
AWS_DEFAULT_REGION (us-east-1)
AWS_SECRET_ACCESS_KEY

Keep a copy of the access key and secret, then use them to authenticate using the CLI:

```
aws configure
```

Region: us-east-1 (London)

##  Create an S3 bucket for Terraform state storage

```
aws s3api create-bucket  \
  --bucket dbrown-terraform-state-bucket \
  --create-bucket-configuration LocationConstraint=us-east-1

aws s3api put-bucket-versioning \
  --bucket dbrown-terraform-state-bucket \
  --versioning-configuration Status=Enabled

aws s3api put-bucket-encryption \
  --bucket dbrown-terraform-state-bucket \
  --server-side-encryption-configuration '{
    "Rules": [{
      "ApplyServerSideEncryptionByDefault": {
        "SSEAlgorithm": "AES256"
      }
    }]
  }'
  ```

## Create an ECR to store the Docker images

Create an ECR repository at https://us-east-1.console.aws.amazon.com/ecr/private-registry/repositories/create?region=us-east-1

Example URL: https://746867312608.dkr.ecr.us-east-1.amazonaws.com/nodejs-terraform

## Terraform configuration

Use pre-existing AWS security group, VPC and subnets:

### Security group 

https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#securityGroups:

### VPC

https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#vpcs:

### Subnets

https://us-east-1.console.aws.amazon.com/vpcconsole/home?region=us-east-1#subnets:

## References

https://medium.com/@pavankalyanmeda5779/deploying-a-node-js-app-on-aws-ecs-fargate-with-terraform-and-github-actions-b6463d4a07fe