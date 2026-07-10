# nodejs-terraform

https://medium.com/@pavankalyanmeda5779/deploying-a-node-js-app-on-aws-ecs-fargate-with-terraform-and-github-actions-b6463d4a07fe

Create AWS IAM user with CLI and AdministratorAccess rights.

Create S3 bucket for Terraform:

aws s3api create-bucket  \
  --bucket dbrown-terraform-state-bucket \
  --create-bucket-configuration LocationConstraint=eu-west-2

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

Use pre-existing security group, VPC and subnets:

Security group 

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#securityGroups:

VPC

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#vpcs:

Subnets

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#subnets:

ECR

Create ECR repository at https://eu-west-2.console.aws.amazon.com/ecr/private-registry/repositories/create?region=eu-west-2

URL:
https://746867312608.dkr.ecr.eu-west-2.amazonaws.com/nodejs-terraform-app