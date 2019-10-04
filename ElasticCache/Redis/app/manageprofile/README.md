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
