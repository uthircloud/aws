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

<B>Converting .pem file to .ppk file. </B>

Once PuttyGen is downloaded execute its exe file it will launch puttygen window.

![OpenPuttyGen](https://user-images.githubusercontent.com/50639924/66003076-1f5be980-e473-11e9-965e-9435e397da46.PNG)

Click **File->LoadPrivate Key**

Navigate to your local directory in which you have stored your .pem file of the downloaded keypair.

![PrivateKeySelect](https://user-images.githubusercontent.com/50639924/66003286-a6a95d00-e473-11e9-94b6-a1b3e34a17a1.PNG)

In the File Name section select box change file type to All Files this will show the .pem file from the selected directory.

![Keypair-Select](https://user-images.githubusercontent.com/50639924/66003495-40710a00-e474-11e9-9010-7abfddaece59.PNG)

After the file selection click open it will load the Key and show success message.When prompted click ok and Save private Key in
your local.

![KeyLoad](https://user-images.githubusercontent.com/50639924/66003568-7adaa700-e474-11e9-913b-cdd8f0481fdf.PNG)

It will generaye a .ppk file save it in your local. This file is needed to SSH your instance everytime from here on.

To connect your EC2 instance make sure its in started and running.Once its started copy **IPv4 Public IP** address of your instance. We need this IP to connect to EC2 instance.

![RunnEc2](https://user-images.githubusercontent.com/50639924/66121134-71ebf180-e5aa-11e9-9f60-1e3b166733f6.PNG)

Open putty and use this IP address with default user name like <B>ec2-user@<IPv4 Public IP></B>

![PuttyConne](https://user-images.githubusercontent.com/50639924/66121338-f0489380-e5aa-11e9-84ce-653507b8cfb8.PNG)

Now navigate to <B>Connection->SSH->Auth</B> click Browse and refer your save .ppk file and click open.

![PuttyConne](https://user-images.githubusercontent.com/50639924/66121861-29353800-e5ac-11e9-82aa-bafd1ec18f4f.PNG)

If evrything is configured correctly it will prompt to open window. Click Yes and you will be getting connected to EC2.

Now all set to run any application on EC2.

As a best practice always update your EC2 instance image for the first time when you connect.To update your EC2 image run below comment.

<B>sudo yum update -y </B>

From here on you can update anyother software which you want to run and run your application. For instance if you want to run java program update java using below command.

<B>sudo yum install java-1.8.0 -y</B>

**Create an EC2 instance using Cloud Formation**

**YAML**

EC2-Instance-Serer:
Type: AWS::EC2::Instance
Properties: 
  AvailabilityZone: us-east-1b
  ImageId: ami-00068cd7555f543d5
  InstanceType: t2.micro
  SecurityGroups: 
    - !Ref EC2-Security-Group
   
EC2-Security-Group:   
Type: AWS::EC2::SecurityGroup
Properties: 
  GroupDescription: EC2-Security Group defines rules for inbound and outbound
  GroupName: ec2-server-security-group
  SecurityGroupEgress: 
    - FromPort: 65.27.244.128/32
    - IpProtocol: tcp
    - ToPort: 22
