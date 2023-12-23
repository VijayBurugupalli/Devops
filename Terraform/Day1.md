# Infrastructure as a Code
### Definition
Infrastructure as code is a way of **managing and provising** the code using code instead of doing it manually.

You can write all the configurations and provisional requirements to maintain the infrastructure all the time in a code format. Then you can version control all the configuration and provisional code along with the documentation required, it helps you avoid undocumented and ad-hoc configuration changes.

### Declarative vs Imperative
There are two ways to approach IAC. They are :
1. Declarative 
1. Imperative
##### Declarative Approach:
The approach used to create the desired state of the system, including the resources we need and the properties we should maintain through out.It can be achieved by IAC tools.
#### Imperative Approach:
An imperative approach instead defines the specific commands needed to achieve the desired configuration, and those commands then need to be executed in the correct order. 

#### Note
Many IaC tools use a declarative approach and will automatically provision the desired infrastructure. If you make changes to the desired state, a declarative IaC tool will apply those changes for you. An imperative tool will require you to figure out how those changes should be applied.

IaC tools are often able to operate in both approaches, but tend to prefer one approach over the other.
### Benefits
##### Benefits:
1. Cost reduction
1. Increase in speed of deployments
1. Reduce errors 
1. Improve infrastructure consistency
1. Eliminate configuration drift
### Tools
There are many tools used to achieve IAC. Here are some of the popular tools:
* Puppet
* Chef
* Ansible
* AWS Cloud Formation
* Terraform
  
Howerver, **Terraform** is the most used IAC tool in the current Industrial market.
