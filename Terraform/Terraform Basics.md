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

## Terraform Providers
Terraform providers are the plugins that are used in terraform in order to create the resources. Here are some of the popular providers:
* AWS
* Azure
* GCP
* Alibaba
* Kubernetes
* Oracle

Terraform can also be used with multiple resources and multiple providers, in case of multiple resources use **alias** to specify a particular resource.
## Terraform Variables
Terraform variables are used when we need to parameterize the values of resources so that we don't need to hard code same code every time. There are two types of variables in terraform
1. Input Variables
2. Output Variables
### 1.Input Variable
Input variables are used to give a paramneterized input while creating a resource in terraform. It can be a local input variable or it can be created in seperate vaiables.tf file.
**local**
```
locals {
 ami  = "ami-0d26eb3972b7f8c96"
 type = "t2.micro"
 tags = {
   Name = "My Virtual Machine"
   Env  = "Dev"
 }
 subnet = "subnet-76a8163a"
 nic    = aws_network_interface.my_nic.id
}
 
resource "aws_instance" "myvm" {
 ami           = local.ami
 instance_type = local.type
 tags          = local.tags
 
 network_interface {
   network_interface_id = aws_network_interface.my_nic.id
   device_index         = 0
 }
}
 
resource "aws_network_interface" "my_nic" {
 description = "My NIC"
 subnet_id   = var.subnet
 
 tags = {
   Name = "My NIC"
 }
}
```
**different**
```
variable "ami" {
 type        = string
 description = "AMI ID for the EC2 instance"
 default     = "ami-0d26eb3972b7f8c96"
 
 validation {
   condition     = length(var.ami) > 4 && substr(var.ami, 0, 4) == "ami-"
   error_message = "Please provide a valid value for variable AMI."
 }
} 

variable "type" {
 type        = string
 description = "Instance type for the EC2 instance"
 default     = "t2.micro"
 sensitive   = true
}
 
variable "tags" {
 type = object({
   name = string
   env  = string
 })
 description = "Tags for the EC2 instance"
 default = {
   name = "My Virtual Machine"
   env  = "Dev"
 }
}
 
variable "subnet" {
 type        = string
 description = "Subnet ID for network interface"
 default     = "subnet-76a8163a"
}
```
```
resource "aws_instance" "myvm" {
 ami           = var.ami
 instance_type = var.type
 tags          = var.tags
 
 network_interface {
   network_interface_id = aws_network_interface.my_nic.id
   device_index         = 0
 }
}
 
resource "aws_network_interface" "my_nic" {
 description = "My NIC"
 subnet_id   = var.subnet
 
 tags = {
   Name = "My NIC"
 }
}
```
### 2.Output Variables
Output variables in Terraform are used to display the required information in the console output after a successful application of configuration for the root module. To declare an output variable, write the following configuration block into the Terraform configuration files.
```
output "instance_id" {
 value       = aws_instance.myvm.id
 description = "AWS EC2 instance ID"
 sensitive   = false
}
```
## Conditional Expression
A conditional expression uses the value of a boolean expression to select one of two values.
`condition ? true_val : false_val`
