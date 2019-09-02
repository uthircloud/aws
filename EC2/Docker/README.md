# Installing Docker in AWS EC2

Pre-Requisite: You should have running EC2 instance and have SSH access to the instance.

After login to EC2 using SSH (Puytty) change user to sudo user by executing below command.

**[ec2-user@ip-yyy-yyy ~]$ sudo su**


This will change the ec2-user as root user.

**[root@ip-yyy-yyy ec2-user]#**

Update EC2 instance to make sure to have latest patches available.

**[root@ip-yyy-yyy ec2-user]# yum update -y**

You can see updates in logs at the end you can get updated message like below.

**Updated:**  
  **amazon-linux-extras.noarch 0:1.6.9-1.amzn2** 
  **amazon-linux-extras-yum-plugin.noarch 0:1.6.9-1.amzn2**  
  **amazon-ssm-agent.x86_64 0:2.3.662.0-1.amzn2**  
  **curl.x86_64 0:7.61.1-11.amzn2.0.2**  
  **ec2-hibinit-agent.noarch 0:1.0.0-4.amzn2**  
  **ec2-instance-connect.noarch 0:1.1-10.amzn2**  
  **libcurl.x86_64 0:7.61.1-11.amzn2.0.2**  
  **libssh2.x86_64 0:1.4.3-12.amzn2.2.1** 
  **nss-softokn.x86_64 0:3.36.0-5.amzn2.0.1**  
  **nss-softokn-freebl.x86_64 0:3.36.0-5.amzn2.0.1**
  **systemtap-runtime.x86_64 0:4.1-0.20190208git4e76869512d2.amzn2.0.2** 

**Complete!**

Now we have latest version of AMI is updated. Next step is to install docjker in EC2.Execute below command to install docker.

**[root@ip-yyy-yyy ec2-user]# yum install docker -y**

You can see logs of installation after above command is executed. At the end you can see confirmation of installation like below.

**Installed:**  
  **docker.x86_64 0:18.06.1ce-10.amzn2**  

**Dependency Installed:**  
  **libcgroup.x86_64 0:0.41-15.amzn2  libtool-ltdl.x86_64 0:2.4.2-22.2.amzn2.0.2**  
  **pigz.x86_64 0:2.3.4-1.amzn2.0.1**  

**Complete!**

Next to start Doceker execute below command

**[root@ip-yyy-yyy ec2-user]# service docker start**

After successful start of docer we can see below logs.

**Redirecting to /bin/systemctl start docker.service**

Next, add the ec2-user to the docker group so you can execute Docker commands without using sudo.
After this step you have to logout and login agin to take this change effect.

**[root@ip-yyy-yyy ec2-user]# usermod -a -G docker ec2-user**  
**[root@ip-yyy-yyy ec2-user]# exit**

If everything is correct after re-login when executing below command you can see some info logs in ec2-user login.

**[ec2-user@ip-yyy-yyy ~]$ docker info**

**Kernel Version: 4.14.123-111.109.amzn2.x86_64**  
**Operating System: Amazon Linux 2**  
**OSType: linux**  
**Architecture: x86_64**  
**CPUs: 1**  
**Total Memory: 983.7MiB**  
**Name: ip-yyy-yyy.us-west-2.compute.internal**  
**ID: CD4R:TZQ2:N3BZ:TSM6:SQOK:JNWZ:FRIC:3F2P:LG3F:EFVY:FUIQ:QEYE**  
**Docker Root Dir: /var/lib/docker**  
**Debug Mode (client): false**  
**Debug Mode (server): false**  
**Registry: https://index.docker.io/v1/**  
**Labels:**  
**Experimental: false**  
**Insecure Registries:**  
 **127.0.0.0/8**  
**Live Restore Enabled: false**  


Now we are all set to run our first conatainer/app in Docker insider AWS-EC2

Run below command to pull and run python training app.

**[ec2-user@ip-yyy-yyy ~]$ docker run -d -p 80:5000 training/webapp:latest app.py**

After successful execution of above command you can see below logs. 

**Unable to find image 'training/webapp:latest' locally**  
**latest: Pulling from training/webapp**  
**e190868d63f8: Pull complete**  
**909cd34c6fd7: Pull complete**  
**0b9bfabab7c1: Pull complete**  
**a3ed95caeb02: Pull complete**  
**10bbbc0fc0ff: Pull complete**  
**fca59b508e9f: Pull complete**  
**e7ae2541b15b: Pull complete**  
**9dd97ef58ce9: Pull complete**  
**a4c1b0cb7af7: Pull complete**  
**Digest: sha256:06e9c1983bd6d5db5fba376ccd63bfa529e8d02f23d5079b8f74a616308fb11d**  
**Status: Downloaded newer image for training/webapp:latest**  
**76d8519d81834e81ed7b788de9569254dadcbc2bf66a21addcbc71119d6f4225**  


This command will pull latest version of trainning python app and run. In the command flag -p 80:5000 tells Docker to link port 5000 on the Docker container to port 80 on the EC Instance.  

Now we can test this app using below curl command in docker.

**[ec2-user@ip-yyy-yyy ~]$ curl http://localhost**

If this command execution was successful we can see below logs.  

Hello world![ec2-user@ip-yyy-yyy ~]$

We can access the same application in browser with our EC2 instace IP.

**Reference** [Running Docker in AWS](https://www.ybrikman.com/writing/2015/11/11/running-docker-aws-ground-up/#installing-docker)














 

