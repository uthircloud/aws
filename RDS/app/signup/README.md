# Connecting Oracle DB using Spring Boot Application

This article give overview of connecting a Oracle Data base using Spring Boot application.

**Prerequisite**

 - Java IDE of your choice.In this example we are using STS.
 - Maven
 - Oracle Data Base. In this example Oracle data base is created in AWS Cloud.To create a AWS-RDS DB refer below link.
   https://github.com/uthircloud/aws/tree/master/RDS
   
 
 ## Create a sample application named singnup
 
 To create sample maven application use spring initializr it will create quick template app as per our need with given
 dependencies.
 
 Click below link
 
 https://start.spring.io/
 
 Give Group and Artifact name as per your project name.
 
 ![Bootstrat](https://user-images.githubusercontent.com/50639924/65980809-de99ab80-e445-11e9-9ce9-3decb69e84ae.PNG)
 
 Choose dependencies for your project by typing your dependcy keyword. In this case as we creating a
 REST application with DB connection we need Web,JPA dependencies.Type these two dependencies individualy and add them one by one.
 Click Generate it will crate a sample templeate project and download to your local.
 
 ![Dependency](https://user-images.githubusercontent.com/50639924/65981012-3e905200-e446-11e9-9a68-59054e2ebb89.PNG)
 
 ![Generate](https://user-images.githubusercontent.com/50639924/65981241-b1013200-e446-11e9-9598-9a528fc40c78.PNG)
   
 
 

