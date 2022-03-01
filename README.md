# Learn Terraform data sources - VPC

Learn how Terraform data sources help you import data into your Terraform configuration.

Follow along [with this
tutorial](https://learn.hashicorp.com/tutorials/terraform/data-sources?in=terraform/configuration-language)
on HashiCorp Learn.


## This repo contains configuration to deploy infrastructure in AWS -VPC and security groups for application which can be deployed from [this repo](https://github.com/krasteki/terraform-data-sources-app.git)


Data sources used:
[`aws_availability_zones`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones) - part of the AWS provider, In this case, the `state` argument limits the availability zones to only those that are currently available.
[`aws_region`](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/region) eu-west-2



### Prerequisites

- Terraform (version used v1.1.6) - Check [here](https://learn.hashicorp.com/tutorials/terraform/install-cli) for install instructions.
- AWS subscription - Check [here](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all) for AWS Free Tier.
- Before you can build the infrastructure, you need to provide your AWS credentials to Terraform as environment variables. You can create AWS credentials on [this page](https://console.aws.amazon.com/iam/home?#security_credential).

**Note**:Some of the infrastructure in this configuration may not qualify for the AWS free tier. Destroy the infrastructure at the end of the guide to avoid unnecessary charges.


### Setup Instructions


#### I. Clone the repo

```
$ git clone https://github.com/krasteki/terraform-data-sources-vpc.git
$ cd terraform-data-sources-vpc
```

#### II. Authenticate to AWS

```
$ export AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY
$ export AWS_SECRET_ACCESS_KEY=YOUR_SECRET_KEY
```

**Note**: You may need to also export your `AWS_SESSION_TOKEN` and `AWS_SESSION_EXPIRATION` as **environment variables**.

#### III. Run the following commands in the cloned folder:

1. `$ terraform init` - Initializing a configuration directory downloads and installs the providers defined in the configuration, which in this case is the aws provider.
2. `$ terraform fmt` - Automatically updates configurations in the current directory for readability and consistency. Format the configuration. Terraform will print out the names of the files it modified, if any. In this case, the configuration file was already formatted correctly, so Terraform won't return any file names.
3. `$ terraform validate` - Validates the configuration.
4. `$ terraform plan` - Creates an execution plan, which lets you preview the changes that Terraform plans to make to the infrastructure.
5. `$ terraform apply` - Creates the infrastructure.


##### The given output values 

The given output values will be saved in a newly generated `terraform.tfstate` file which can be used as a [`terraform_remote_state`]( https://registry.terraform.io/providers/hashicorp/terraform/latest/docs/data-sources/remote_state) for [`application`](https://github.com/krasteki/terraform-data-sources-app.git)


#### IV.Destroy configuration

**Note**: If the [application](https://github.com/krasteki/terraform-data-sources-app.git) workspace is deployed You must destroy it before remove the resources in this configuration. `terraform_remote_state` data source share data between the two workspaces and they need to be destroyed by the last created order.

`$ terraform destroy`
