# aws-infra

We have 4 main files here

The provider.tf contains the provider and region details

The variables.tf contains all the variables, their types and their default values.

The main.tf contains all the resources which are to be created.

The variables.tfvars is a file which passed in the command prompt to take the values like cidr blocks region etc.

To run the terraform configuration files, we have to run the following commands
1. **terraform init**  -  this command initializes the backend processes and makes the ground ready for creation.
2. **terraform apply** - this command creates all the resources listed in the config files. Before creation a confirmation is asked.
3. **Terraform destroy** - this command destroys all the created and active resources

Here, we have created 1 vpc, 3 private subnets and 3 public subnets in different availability zones but same region, 1 public route table, one private route table and 1 internet gateway.

We have included .tfvars and .terraform.lock.hcl and terraform.state in the gitignore file.

# aws-infra

Assignment 4



Prerequisites: In this assignment we are setting up networking infrastructure using terraform on AWS. For that we have installed AWS CLI and terraform

Requirements and Description: users "aws_cli_dev" and "aws_cli_demo" have been created in dev and demo aws user accounts with administrator access respectively.
Now we create access keys under the security credentials of the users and configure them in the AWS CLI for each of the dev and demo profiles.

Steps to run the project:

The below commands are used to setup the virtual private cloud (vpc) network infrastructure in the AWS region as per inputs provided


1. "terraform init" - Initializes the backend and provider plugins hashicorp/aws
2. "terraform fmt" - Formats the terraform files in the directory
   
3. "terraform apply" -var-file var.tfvars" - It will setup the vpc with subnets (public and private) with the internet gateway as per the configuration provided in the main.tf file. The data.tf file contains the Availability Zones data source allows access to the list of AWS Availability Zones which can be accessed by an AWS account within the region configured in the provider. The "-var-file var.tfvars" helps in executing the application with the values defined in the var.tfvars file for the vpc cidr block, public and private subnets, profile and aws_region.
4. The EC2 instance is created in the VPC created and is attached to the github secrets configured
   
5. "terraform destroy" -var-file var.tfvars" - It will destroy the network infrastructure setup on AWS.


Assignment 6:

Registering a Domain Name:

Go to Namecheap or any other domain registrar and register a domain name. If you're a student, you can get a free .me TLD domain from Namecheap with the Github Student Developer pack.

Configuring Amazon Route 53:

1. Log in to your AWS account and go to the Amazon Route 53 console.
2. Create a public hosted zone for your domain name by clicking on "Create Hosted Zone" and entering your domain name (e.g. yourdomainname.tld) in the "Domain Name" field. Leave the other fields as default and click on "Create Hosted Zone."
3. After creating the hosted zone, you will see four Route 53 name servers listed for your hosted zone. Copy these name servers to use in the next step.
4. Go to Namecheap or your domain registrar's console and update the domain's name servers to the Route 53 name servers you copied in the previous step.
5. Create a subdomain and hosted zone for the dev AWS account by clicking on "Create Hosted Zone" again and entering "dev" in the "Name" field and selecting "Public Hosted Zone" in the "Type" field. Enter your domain name (e.g. yourdomainname.tld) in the "Domain Name" field and leave the other fields as default. Click on "Create Hosted Zone."
6. After creating the dev hosted zone, you will see four Route 53 name servers listed for the hosted zone. Copy these name servers to use in the next step.
7. Go back to the hosted zone for your main domain name and click on "Create Record Set." Enter "dev" in the "Name" field, select "A - IPv4 address" in the "Type" field, and enter the IP address of your dev server in the "Value" field. Leave the other fields as default and click on "Create."
8. Create a subdomain and hosted zone for the demo AWS account by repeating steps 5-7, replacing "dev" with "prod."

Assignment9

The command which we are using to upload the namecheap ssl certificate to aws is given below

$ aws --profile demo acm import-certificate --certificate fileb://Certificate.pem
      --certificate-chain fileb://CertificateChain.pem
      --private-key fileb://PrivateKey.pem

I replaced the file paths with my file path with extension names to upload the certificate.

Added 2 seperate kms keys one for ebs volumes encryption and the other for rds instance encryption.

Modified load balancer security group ingress rule to run on port 443(https).
