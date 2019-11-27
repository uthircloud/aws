AWS-Security Best Practices White paper
---------------------------------------
Shared Responsiblity Model

AWS is responsible for
 - Facilities
 - Phisical security of hardware
 - Network infra
 - Virtualization of infra
 
Consumer is Responsible for
 - AMI
 - OS
 - Applications
 - Data in transit
 - Data at Rest
 - Data Stores
 - Credentials
 - Plocies and config

IAM Service
------------
  - Used to manage different Users in same AWS account
  - Always create IAM user and password which provide access key use it as a best practice.

AWS Global Infrastructure

Regions -> Multiple AZ -> Multiple Data Centers

 - Each regions consist of min of 2 AZ
 - Data Stored in one Region wont be available in another regions. Its responsibility of consumer to replicate it to other regions
 - AZ are designed for fault tolerance. 

1.Infrastructure Services
  - EC2,EBS,AutoScaling,VPC
  - Compute resources will be responsibility of AWS 
  - OS and Access Control is responsibility of customer
2.Container Services
  - In this category AWS will manage OS and platform layer of this kind of services.
  - RDS,AWS Elastic Map Reduce,BeanStalk
  - Consumer responsible for setting up network control like firewall rules and managing platform level identity and access management seperately from IAM.
3.Abstracted Service
  - In this category services fully managed by AWS as consumer we will access this services using API' s or CLI and create our own apps using this abstraction services.
  - S3,Glacier,DynamoDB,Email Service (SES)
  
 **Shared Responsiblity Model**
 
 **1. Infrastructure Service**
 In a shared responsibility model consumer owns OS but AWS helps to bootstrap the initial access to OS.
 
 When launching EC2 use must be authenticated to Access the instance.
 
 - To Authenticate user to EC2 AWS provide industry standard Aysmetric Key pairs which consist of Public and Private key called EC2 key pairs.
 - EC2 key pairs is different from AWS account credentials and IAM user credentilas these are specific to EC2 instance.
 - In AWS we can create Key pairs in 2 ways. 1. User generated 2. AWS generated EC2 key pairs.
   When using AWS EC2 key pairs both public and private Key is presented to User. AWS will store only public key. User is responsible for providing private key during access.
   Once key is lost user needs to generate new key.
 - For Linux AMI's public key is stored in OS users's ~/.ssh/authorized_keys file.
 - For Windows using ec2config service it sets a new random admin password for the instance and encrypt using  AWS EC2 public key. Then user can use AWS conole or CLI tools by providing
   EC2 public key to decrypt the password.This password along with default admin account for EC2 instance can be used to access the instance.

**2. Container Service**
In container service OS and Infra will be responsibiity of AWS. Consumer is responsible for manging access to the services like defining Firewall rules and IAM user based access. 

 - In case of RDS-Oracle DB is managed by AWS. User is responsible for controlling access to it using security rules and IAM policies and securing data like encrypting etc.
 
 **3. Abstracted Service**
 In abstracted services Infra layer,OS,Platform all managed by AWS. Consumer will accees this services using API endpoints or CLI tools.
  - In case of S3 and DynamoDB user can control its access using IAM and ACL policies.Also data can be encrypted at rest and in transit.
  
 **AWS Trusted Advisor Tool**
 
 AWS premium plan includes Trusted Adviosr tool which helps to identify security misconfigurations.
 
 For instance in EC2 its will check
   - Limited access to ports like SSH(22),TelNet(23),RDP(3389),VNC(5500)
   - Limited access to common DB's MSSQL(1434),MySQL(3306),Oracle(1521),PostgreSQL(5432)
   - IAM is configured to access to AWS services
   - MFA is enabled to account to provide 2FA
   


