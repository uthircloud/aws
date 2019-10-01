# Create/Launch EC2 instance

## Launc EC2 instance
LogIn to AWS account using IAM user and type EC2 in dash board search box.

![Select-EC2](https://user-images.githubusercontent.com/50639924/65999377-457d8b80-e46b-11e9-8157-295d60cd2d41.PNG)

**Select LaunchInstance**

![Select-EC2](https://user-images.githubusercontent.com/50639924/65999470-78278400-e46b-11e9-85e1-4cd400e17213.PNG)

**Select Linux 2 AMI**

![Select-EC2](https://user-images.githubusercontent.com/50639924/65999588-ae650380-e46b-11e9-856d-3743c977b06a.PNG)

**Choose Free tier t2.micro instance and click Configure Instance Details**

![T2-Micor](https://user-images.githubusercontent.com/50639924/65999771-1287c780-e46c-11e9-811f-573083d6faf1.PNG)

**Do not change any default configuration in this page then  click Add Storage**

![ConfigDetails](https://user-images.githubusercontent.com/50639924/66000022-993ca480-e46c-11e9-9dd5-d47d50f2618e.PNG)

![ConfigDetails-2](https://user-images.githubusercontent.com/50639924/66000044-a3f73980-e46c-11e9-8b4f-c5bc5437f4bf.PNG)

**Do not change default storage in storage tab click Review and Launch**
![Storage](https://user-images.githubusercontent.com/50639924/66000240-03554980-e46d-11e9-97f4-53de97e67733.PNG)

**Choose Create Newkeypair and download the keypair keep the .pem file in your local it require to connect EC2** 
![KeyPair](https://user-images.githubusercontent.com/50639924/66000495-85de0900-e46d-11e9-9846-0a3a6e3e61ca.PNG)

**Once its downloaded launch instance**

Once its launched you can see your instance.
![LaunchingInstance](https://user-images.githubusercontent.com/50639924/66000790-2e8c6880-e46e-11e9-9b59-c164b2cec69c.PNG)

Name your instance
![Name-ec2](https://user-images.githubusercontent.com/50639924/66000973-8cb94b80-e46e-11e9-8632-e68f18528bb0.PNG)

<B>
When launching EC2 in this way AWS will create some default configurations. We can change this configurations as per our needs depending on type of usage of EC2.For example AWS will create default Security Group,VPC,Subnets.
</B>


## Connect to EC2 instance from Windows 10

We can connect EC2 instance throuh SSH. To connect via SSH we need to have Putty and PuttyGen.This tools can be
downloaded from below path.

https://www.putty.org/
https://www.puttygen.com/


To connect to EC2 instance from Windows 10 we need to refer the downlaoded key pair. Key pair contains .pem file this needs to be first converted to .ppk file.

**Converting .pem file to .ppk file.


