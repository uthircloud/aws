# Creating AWS-RDS Oracle Data Base and Connecting it using Spring Boot Application.

This article will give detailed overview of Creation of RDS Oracle DB and connecting it using Spring Boot application.

**Prerequisite**

  - You should have valid AWS Account or valid IAM user who can able to create RDS DB.
  - Java IDE of your choice. In this example we are using STS.
  - DB Client to connect to Oracle DB.In this example we are using DBeaver.
  
  ## Create RDS Oracle DB
  
  Login to AWS console using your credentails. Use IAM user instead root account.
  Type RDS in console search box.Make sure you have selected specific region in which you want to create DB.
  
  ![AWS_Conslole-LogIn](https://user-images.githubusercontent.com/50639924/65958173-cc574780-e41c-11e9-85fb-9cbf6bb4951d.PNG)
  
  Click RDS it will open RDS home page.
  
  ![RDS-Home](https://user-images.githubusercontent.com/50639924/65958278-06c0e480-e41d-11e9-975c-b440777791f2.PNG)
  
  **Scorll down and find Create Database. **
  
  ![CreateDB](https://user-images.githubusercontent.com/50639924/65958415-54d5e800-e41d-11e9-83f3-e2bf9cffa7a4.PNG)
  
  **Choose Standard and DB of your choice in our case we choose Oracle.By Choosing Standard we can customize DB instance creation**.
  
  ![ChooseOracle](https://user-images.githubusercontent.com/50639924/65958569-ad0cea00-e41d-11e9-98bd-5e9d8b0656b6.PNG)
  
  **Choose Oracle Standard Edition**
  
  ![StandardEdition](https://user-images.githubusercontent.com/50639924/65958749-26a4d800-e41e-11e9-9472-59519ee8222a.PNG)
  
  **Choose Free-tier**
  
  ![FreeTier](https://user-images.githubusercontent.com/50639924/65958832-5f44b180-e41e-11e9-877b-d55808ce5abe.PNG)
  
  **Give DB instance name,User Name and Password. This is the information which we used to connect this DB instance from application
  and through client.**
  
  
![CredentialSettings](https://user-images.githubusercontent.com/50639924/65959136-383aaf80-e41f-11e9-88d6-d17459cfaf1e.PNG)

**Choose instance size as default values.In size section un check autoscaling as its not needed for testing purpose**

![InstanceSize](https://user-images.githubusercontent.com/50639924/65959490-23aae700-e420-11e9-9ff2-2516fd210035.PNG)

![Storage](https://user-images.githubusercontent.com/50639924/65959499-2a395e80-e420-11e9-995e-a5be286ba0c6.PNG)

**Choose to have default values in Availability and Connectivity**

![Availability-Connetion](https://user-images.githubusercontent.com/50639924/65959696-ab90f100-e420-11e9-8d3c-97112f5d440d.PNG)

**In Connectivity section click Addition Connetivity Configuration and choose Publicly accessible to Yes and VPC Security Group-Create New
  This will create a new Security Group and make instance accessible public as we want to access this instance from anywhere**
  
  **This configuration is only for testing purpose for PROD environments its advisable not to enable Public access**
  
  ![Additional-Config](https://user-images.githubusercontent.com/50639924/65961502-bd749300-e424-11e9-9aa5-8fcf3d5b434d.PNG)
  
  ![Port](https://user-images.githubusercontent.com/50639924/65960271-1c84d880-e422-11e9-8afe-ff58c833a617.PNG)
  
  <b>Click Additional Configuration and give Initial DB name of your choice. This name will be used in URL
    Make sure DB name is less than 8 character long </b>
  
  ![DBOptions](https://user-images.githubusercontent.com/50639924/65961560-ded57f00-e424-11e9-81f7-d5afa75c9697.PNG)
  
  **In this section have all other default values and make sure final section describe free tier eligibility**
  
  ![Default1](https://user-images.githubusercontent.com/50639924/65960755-28bd6580-e423-11e9-8d46-865e00424984.PNG)

  ![Default2](https://user-images.githubusercontent.com/50639924/65960766-2eb34680-e423-11e9-8655-228a70759876.PNG)

  ![Default3](https://user-images.githubusercontent.com/50639924/65960775-34109100-e423-11e9-89c8-c557cc2e7085.PNG)
  
  **Click Create Data Base it will create DB in the slected region. This will take few minutes**
  
  ![DB-Creation](https://user-images.githubusercontent.com/50639924/65961908-8fdc1980-e425-11e9-8a69-8b90cd79e53c.PNG)