Terraform IAC Basics

    In order to write Terraform code these are the main things we define
    ................................................................................
    .................................................................................
    Provider  - the provider name like aws or azure,gcp then plugins will be loaded

    Resource - Resource block is where we define resources like ec2, vpc or eks any other service in specific provider

    variables - Instead of hardcoding the values in the main.tf we use variables file and define variables inside this file


    output  - Output file we difine values which are to be displayed during plan or apply example vpc id.
    ................................................................................
    .................................................................................


State file - Terraform keeps track of the resources it created in a file called state file. This file is used to know the current state of the resources and to know what resources are created and what are not.

Statefile Management - Terraform state file can be stored in local or remote. If we store in local then we need to take care of the state file and if we store in remote then terraform cloud or s3 bucket can be used to store the state file.

StateFile Locking - Terraform state file can be locked so that only one person can run the terraform apply or plan at a time. This is to avoid the conflicts in the state file.

Dynamo Db - Terraform state file can be stored in dynamo db also. This is used to lock the state file so that only one person can run the terraform apply or plan at a time.

Terraform Cloud - Terraform cloud is a service provided by hashicorp to store the state file and to run the terraform code. This is used to store the state file and to run the terraform code in the cloud.


Terraform Modules - Terraform modules are used to reuse the code. We can define the code in the module and we can call the module in the main.tf file. This is used to reuse the code and to make the code more readable.

Example - We can define the vpc code in the module and we can call the module in the main.tf file. This is used to reuse the code and to make the code more readable.

...................................................................................................


Now lets create a Terraform Iac setup for creating a VPC in AWS and use moduler approach to create the VPC.

```

Imortant files for above are main.tf, variables.tf, output.tf, vpc.tf, provider.tf, terraform.tfvars, versions.tf

main.tf - This is the main file where we call the module vpc

variables.tf - This is the file where we define the variables

output.tf - This is the file where we define the output values
provider.tf - This is the file where we define the provider

terraform.tfvars - This is the file where we define the values for the variables

versions.tf - This is the file where we define the terraform version

```

How to configure AWS credentials for Terraform

1. Login to AWS console with devops user which has administrator access policy attached.
2. go to credentials and create a new access key and secret key for the user.
3. Download the access key and secret key in a file called credentials in
4. Downlaod and install AWS CLI and configure the credentials file in ~/.aws/credentials file.
5. link for AWS CLI installation - https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html



Procedure to install aws cli in windows
...................................................................................
..................................................................................
To download and install AWS CLI on windows use the below command 
 curl "https://awscli.amazonaws.com/AWSCLIV2.msi" -o "AWSCLIV2.msi"
Install manually by double clicking the file.
add path to environment variables under system path C:\Program Files\Amazon\AWSCLIV2
Then run aws configure and provide the access key and secret key.
if you have installed AWS CLI then you can check the credentials file in ~/.aws/credentials file.
ls ~/.aws/credentials
cat ~/.aws/credentials
...................................................................................
..................................................................................



Remoate backend for terraform state file

problem and solution - If we are using local backend for terraform state file then we need to take care of the state file and if we are using remote backend then we can store the state file in s3 bucket or terraform cloud.
solution - We can use s3 bucket to store the state file and we can use dynamo db to lock the state file.


Install terraform in windows
...................................................................................
..................................................................................
steps to install terraform in windows
curl -LO "https://releases.hashicorp.com/terraform/1.1.4/terraform_1.1.4_windows_amd64.zip"
unzip terraform_1.1.4_windows_amd64.zip
mkdir -p /c/terraform
mv terraform.exe /c/terraform/
Add environment variable - Click "New" and add the path C:\terraform.
reopen git bash
terraform -version
...................................................................................
..................................................................................

Terraform commands
 terraform init
 terraform plan
 terraform apply
    terraform destroy


VPC
  IGW
  private subnet
  routtable - igw to public subnet
  public subnet
    routtable - private subnet to public subnet
    nat gateway

When ever we are writing calculator code we use a + b instead of hardcoding values, same way we use variables in terraform code.
Variables are used to make the code more readable and to reuse the code.

In modules we dont need to 

rm -rf .terraform
terraform init -reconfigure

...................................................................................
..................................................................................

Deploying prcedure in Kubnernetes

spin up an ec2 instacne 
Install docker,kubectl,awscli 

kubectl config view
kubectl config current-context
kubectl config use-context
aws eks update-kubeconfig --region ap-south-1 --name my-eks-cluster
kubectl get all
git clone https://github.com/yvr-vishnu/ultimate-devops-project-demo.git
cd ultimate-devops-project-demo/kubernetes

#Create a servcie acccount
kubectl apply -f serviceaccount.yaml
kubectl apply -f complete-deploy.yaml

#wait untill all pods comes up an running
kubectl get pods
kubectl get svc | grep frontendproxy

with this you can see the IP 172.20.109.199 and port 8080

Since this is private ip we will not be able to access site

we need to create searvice lb for ths

kubectl edit svc opentelemetry-demo-frontendproxy

go to last of the page replace clster Ip with LoadBalancer

It takes some time to create lb in the aws in backend

kubectl get svc | grep forntendproxy

lb public dns name:8080

http://ab8700208c59545b4b6aa8fad2deb98b-1524806230.ap-south-1.elb.amazonaws.com:8080/cart

we should be able to access site now successfully


we will see how to use ingress instead of loadbalancer

LB VS INGREES

LB is not declerative
    Does not allow to use host name of site like aws.com instead we are limited to use public dns name
	https is not allowed
	not be able to have custom features
	LB Cost is more and can't be created for each microservice seperatly
	Only will be able to ALB type in AWS but cant use F5, NGINX
	

...................................................................................
..................................................................................
