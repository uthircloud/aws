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
   

AWS Account - Root Account will have all permission. Its best practice not to use Root Account. Instead create IAM users.
IAM Users   - Under each Account we can create multiple users and provide different kind of access to each user.
Groups      - We can group every users under a specific group's. For each groups we can attach different policies.
Roles       - Roles are attched with policies which allows 3 types of access.
              - Within same Account to access different AWS Resources. Ex from EC2 to S3 bucket.
              - Corss Account Access
              - Federated Identity Access. Using existing corporate user credntial to access AWS resources instead of creating  new IAM users.
              
**Policies**
Policies are permissions or set of rules which define who is authorized to access specific AWS resources.

**Resources Policy**

Users will create Resources and define who will access thes resources by defining or attaching specific policies to the resources.

**Capability Policy**

Company wide polices which is attached to User or Group.

Both **Resources Policy** and **Capability Policy** are cumulative in nature. An usere permission to specific AWS resource is cumulative of this two policies.

**Manage AWS Accounts,IAM Users,Groups,Roles**

*AWS Accounts*

An organization can have either single or multiple AWS account to manage AWS resources.
  - A single AWS account for all regiongs like DEV,TEST,PROD
  - Multiple AWS account for different departments in a single organization
  - Each account will have a root user which is have all the privillages. But as a best practice its advisable to create IAM user under a account and use it for day today activites.
  
**IAM User**
   - We can create different IAM users based on their activites. Ex Developers needs specific set of accesses compare to Testers
   - We can create respective IAM users and specify their access privillages by attaching corresponding polices.
   
**IAM Groups**
    - Groups will consist of collective users. Ideally we will group different users in a single group and each group is have predefined policies attached to it. All users in the group will inherit all the policies specific to that group.
    
**IAM Roles**
    - IAM roles are used for below given 3 different purposes.
    - To give/control access to different AWS resources. Ex an EC2 instance to connect S3 bucket.
    - To give access to cross account access of AWS resources.
    - Identity federation. Ex In a corporate environment users will have identy already like LDAP we can use same idnetity to control AWS resources.
    
**Mange OS level Access to EC2 instance**


     -  To access OS of EC2 instance we need different set of credentials. In AWS this can be done using AWS security key pairs (asymetric key pairs).
     - These keypairs can be created different ways using different industry standards using tool like OpenSSL.
     - Once the key paris is created only public key is loaded in AWS. User will have to store Private Key and have to use it to connect EC2 instance.
     - When using AWS to create Key pairs both public and private keys are presented to user.
     - In case of Linux in AWS using Cloud-init service EC2 AMI is launched EC2 keypair is appended to initial OS user's ~/.ssh/authorized_keys file.
      - In case of WINDOWS ec2config service will create new random password and user should use this along with public key.

**Storing and Managing Encryption Keys in the Cloud**
Tets
    - Facilities
    * In AWS while securing data using encryption Key can be managed by eith by User themself or can use AWS provided AWSCloudHSM (Hardware Security Model). While using this methods this keys can be accessed through highly secure channels like IPSecVPN,VPC or AWS Direct Connect
    * When a user signup for AWSHSM for Key management an AWSCloudHSM appliance is tagged to users VPC. It's users responsibility to manage Cryptographic domain of the AWSCloudHSM. It's a logical spce to manage Keys
    * AWS only responsible for managing health of the appliance. By which AWS don't have any control over user's key
    
