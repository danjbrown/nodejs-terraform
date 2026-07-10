# nodejs-terraform

## Login to AWS with access key and secret

Create an AWS IAM user with CLI and AdministratorAccess rights.

aws configure

##  Create an S3 bucket for Terraform state storage

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

## Terraform configuration

Use pre-existing AWS security group, VPC and subnets:

Security group 

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#securityGroups:

VPC

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#vpcs:

Subnets

https://eu-west-2.console.aws.amazon.com/vpcconsole/home?region=eu-west-2#subnets:

## ECR to store the Docker images

Create an ECR repository at https://eu-west-2.console.aws.amazon.com/ecr/private-registry/repositories/create?region=eu-west-2

Example URL:
https://746867312608.dkr.ecr.eu-west-2.amazonaws.com/nodejs-terraform-app

## Appendix

https://medium.com/@pavankalyanmeda5779/deploying-a-node-js-app-on-aws-ecs-fargate-with-terraform-and-github-actions-b6463d4a07fe