
# Application modernization with MongoDB Atlas and AWS Elastic Beanstalk

## Introduction: 
This is a technical repo to demonstrate the application deployment using MongoDB Atlas and AWS Elastic Beanstalk.
This tuotorial is intended for those who wants to
1. Have a rapid application deployment
2. Test out the features of an application
3. Fail fast in their development cycle
4. Want to try out the AWS Elastic Beanstalk and MongoDB Atlas 

## [MongoDB Atlas](https://www.mongodb.com/atlas) 
MongoDB Atlas is an all purpose database having features like Document Model, Geo-spatial , Time-seires, hybrid deployment, multi cloud services.
It evolved as "Developer Data Platform", intended to reduce the developers workload on development and management the database environment.
It also provide a free tier to test out the application / database features.


## [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.

## Architecture Diagram:
![AWS EBS with MongoDB Atlas](https://github.com/Babusrinivasan76/ebsintegrationwithatlas/blob/main/images/EBS%20Atlas%20Architecture.png)

## Step by Step Instruction for Deployment:

## Step1: Set up the MongoDB Atlas cluster
         
 Please follow the [link](https://www.mongodb.com/docs/atlas/tutorial/deploy-free-tier-cluster) to setup a free cluster in MongoDB Atlas

Configure the database for [network security](https://www.mongodb.com/docs/atlas/security/add-ip-address-to-list/) and [access](https://www.mongodb.com/docs/atlas/tutorial/create-mongodb-user-for-cluster/).

         
## Step2: Set up the Elastic Beanstalk CLI

Set up the Elastic Beanstalk cli based on the your environment using the [link](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-advanced.html)


  
## Step3: Set up the AWS Elastic Beanstalk environment
 
 
 a. Git Clone the code from Repo 
 
         git clone https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB.git
 
        
 b. Select database parameters in .env file (MEANSTACKwithAtlasonAWSEB --> partner-eb-meanstack-atlas --> server --> .env)
  
  Refer the [link](https://www.mongodb.com/docs/guides/atlas/connection-string/) for getting the MongoDB Atlas connection string 
 
  
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBSMeanstackupdatedbs-2.png) 
 
  
 c. Set up the Elastic Beanstalk initialization paramters through eb init command
 
         eb init
 
Parameters for eb init:

a) Select a default region          : 1 [ select the region in which you want to deploy the Elastic Beanstalk]

b) Select an application to use     : default [Create new Application]

c) It appears you are using Node.js. Is this correct?:  "N"

d) Select a platform                :  3) Docker

e) Select a platform branch.        :  default [ie. 1) Docker running on 64bit Amazon Linux 2)]

f) Cannot setup CodeCommit because there is no Source Control setup, continuing with initialization
Do you want to set up SSH for your instances? : default [Y]

g) Select a keypair.                : default
 
 
 
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp10.png)
 
        
 d. Create the environment with 'eb create'.
 
         eb create
 
 a) Enter Environment Name          : default [partner-eb-meanstack-atlas-dev]
 
 b) Enter DNS CNAME prefix          : default [partner-eb-meanstack-atlas-dev]
 
CNAME should be unique. if it gives an option on account of duplicate, select the default option suggested.

Also pls copy and paste the DNS CNAME selected to the code as the private url. Location: "client --> src --> app --> employee.service.ts (line 10)"

Ensure the CNMAE selected and Private URL server names are same.

Refer the below screenshot for further details
 
 c) Select a load balancer type     : default [application]
 
 d) Would you like to enable Spot Fleet requests for this environment? (y/N): default [N]
 
 
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp17.png)
 
 
 e. Ensure the successful creation of environment ( health check error is acceptable) . It will take minimum 10mins to create the environment. 
 
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp16.png)
 
        
 f. Update the configuration parameters for Loadbalancer / listeners
 
 ![](https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB/blob/main/images/16.EBcreateasampleapp14.png)
 
 
 g. Ensure the configuration changes are applied successfully
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp15.png)


## Step4: Test the application

 i. Using the endpoint created by Elastic Beanstalk test the application for CURD operations and ensure the data are reflecting in MongoDB Atlas documents
 
 
sample endpoint:  http://partner-eb-meanstack.us-east-1.elasticbeanstalk.com/

![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBSMeanstackOutput-1.png)

![](https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB/blob/main/images/17.EBSMeanstackupdatedbs-1.png)



## Summary:

 Any contanirized application can be deployed within no time using this template. 
 Instead of ebsdemoapp.zip , you can use your application zip file and deploy the application.
 Pls share your feedback / queries to partners@mongodb.com
 

