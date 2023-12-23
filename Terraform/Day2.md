# Terraform 
Terraform is an infrastructure as code tool that lets you build, change, and version infrastructure safely and efficiently. Terraform is managed by Hashi Corp and the language used in terraform is HCL. It is compatible with all the providers like AWS, Azure, GCP and many more.
## Installation
We can istall the Terraform from the Hashi Corp website by using the following commands on MAC
```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```
## Configuring to AWS
Go to your AWS account >> Root/IAM user >> Security Credentials >> Access Keys >> Copy the Access ID and Secret Access ID
```bash
$ aws configure
$ Access ID
$ Secret Access ID
$ Zone
$ Output Format
```
## Create a Resource
First create a resource by going through documentation provided by Hashi Corp and execute the terraform workflow.
```
resource "aws_instance" "this" {
  ami                     = "ami-0dcc1e21636832c5d"
  instance_type           = "m5.large"
  host_resource_group_arn = "arn:aws:resource-groups:us-west-2:012345678901:group/win-testhost"
  tenancy                 = "host"
}
```
## Terraform States
Terraform workflow has 4 stages **init**, **plan**, **apply** and **destroy**.
#### Terraform init
Terraform init runs a number of initialization tasks to enable Terraform for use in the current working directory. This is usually executed only once per session.
`terraform init`
#### Terraform Plan
This step is like a pre run of your terraform script. It compares all the required infrastructure matches with the available infrastructure and plans for the required changes needs to be made for the deployement.
`terraform plan`
#### Terraform Apply
Terraform apply executes the plan that is created, comparing the current and desired states. This will create or destroy your resources, which means it potentially changes the deployment by adding or removing resources based on changes in the plan. Terraform apply will run the plan command automatically to execute the most recent changes. However, you can always tell it to execute a specific terraform plan command by providing a plan file.
`terraform apply`
#### Terraform Destroy
Terraform destroy will delete all resources that are created/managed by the Terraform environment you are working in.
`terraform destroy`
