# Accessing AWS-Elasticcache (Redis Cache) from Spring Boot application

This article give overview of how to use or access an AWS Redis cache from Spring Boot application.

## Use case

 1. User can create profile and his/her profile will be stored in RDS Oracle DB.
 2. User can able to access his/her profile info from DB.
 3. When getting User profile system first will check Redis cache if the user info is available
    fetch it from cache else fetch it from DB.
    
## Implementation Steps

 1. Create RDS Oracle DB and create User profile specific table.
 2. Create Redis elastic cache using AWS-Elasticcache
 3. Launch an EC2 instance and allow EC2 to connect Redis by changesing its security rule.
 4. Create a Spring Boot application with Oracle DB and Redis implementation.
 5. Run application in EC2 and test Redis cache functionality.
 
 
## 1. Create RDS Oracle DB and create User profile specific table

To create RDS Oracle DB instance follow below link

https://github.com/uthircloud/aws/tree/master/RDS

Once DB instance is created create a table using below script.

<B>
CREATE TABLE UTHIRCLOUDADMIN.user_profile(
    email_id   VARCHAR2(50) PRIMARY KEY,
    first_nm   VARCHAR2(100) NOT NULL,
    last_nm    VARCHAR2(100) NOT NULL,
    middle_nm  VARCHAR2(100),
    dob        DATE NOT NULL,
    create_date_time TIMESTAMP(2) DEFAULT (systimestamp),
    update_date_time TIMESTAMP(2) DEFAULT (systimestamp)
);
 
 </B>
 
## Create Redis Elastic cache using AWS-Elasticcache

To create Redis Elastic cache follow below link

https://github.com/uthircloud/aws/tree/master/ElasticCache/Redis


## Launch an EC2 instance and allow EC2 to connect Redis by changesing its security rule

To launch an EC2 instance follow below link.

https://github.com/uthircloud/aws/tree/master/EC2

One EC2 instance is launched make sure to edit it security group rule to allow port 6379 communication in inbound traffic.
This will enable your EC2 instance to connect Redis cluster which is running in your AWS account.

![InboundRule](https://user-images.githubusercontent.com/50639924/66206303-b5636000-e67d-11e9-9773-2df684671c88.PNG)


