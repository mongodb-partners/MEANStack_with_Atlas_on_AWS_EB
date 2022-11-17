
# Application modernization with MongoDB Atlas and AWS Elastic Beanstalk

## Introduction: 
This is a technical repo to demonstrate the application deployment using MongoDB Atlas and AWS Elastic Beanstalk.
This tutorial is intended for those who want to
1. Have a rapid application deployment
2. Test out the features of an application
3. Fail fast in their development cycle
4. Want to try out the AWS Elastic Beanstalk and MongoDB Atlas 

## [MongoDB Atlas](https://www.mongodb.com/atlas) 
MongoDB Atlas is an all-purpose database having features like Document Model, Geo-spatial, Time-series, hybrid deployment, and multi-cloud services.
It evolved as a "Developer Data Platform", intended to reduce the developers' workload on the development and management of the database environment.
It also provides a free tier to test out the application/database features.



## [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/)
AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.

## Architecture Diagram:
<img width="1037" alt="image" src="https://user-images.githubusercontent.com/101570105/202459877-12832e3e-1960-4b10-b3cd-3bdb71c86111.png">



## Step-by-Step Instruction for Deployment:

## Step1: Set up the MongoDB Atlas cluster
         
 Please follow the [link](https://www.mongodb.com/docs/atlas/tutorial/deploy-free-tier-cluster) to setup a free cluster in MongoDB Atlas

Configure the database for [network security](https://www.mongodb.com/docs/atlas/security/add-ip-address-to-list/) and [access](https://www.mongodb.com/docs/atlas/tutorial/create-mongodb-user-for-cluster/).

         
## Step2: Set up the Elastic Beanstalk CLI

Set up the Elastic Beanstalk cli based on your Operating System using the [link](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install-advanced.html)


  
## Step3: Set up the AWS Elastic Beanstalk environment
 
 
 a. Git Clone the code from Repo 
 
         git clone https://github.com/mongodb-partners/MEANStack_with_Atlas_on_AWS_EB.git
         
        
 b. Select database parameters in .env file and **uncomment** the line.(MEANSTACKwithAtlasonAWSEB --> partner-eb-meanstack-atlas --> server --> .env)
  
  Refer the [link](https://www.mongodb.com/docs/guides/atlas/connection-string/) for getting the MongoDB Atlas connection string 
 
  
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBSMeanstackupdatedbs-2.png) 
 
  
 c. Set up the Elastic Beanstalk initialization parameters through eb init command
 
         cd MEANSTACKwithAtlasonAWSEB/partner-eb-meanstack-atlas
         
         eb init
 
Parameters for eb init:

a) Select a default region          : 1 [ select the region in which you want to deploy the Elastic Beanstalk and note it down for future reference]

b) Select an application to use     :  Create new Application

   Enter the application name : Select the default option.

c) It appears you are using Node.js. Is this correct?:  "N"

d) Select a platform                :  3) Docker

e) Select a platform branch.        :  default [ 1) Docker running on 64bit Amazon Linux 2)]

f) Cannot setup CodeCommit because there is no Source Control setup, continuing with initialization
Do you want to set up SSH for your instances? : default [Y]

g) Select a keypair.                : default
 
 
 
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp10.png)
 
        
 d. Create the environment with 'eb create'.
 
         eb create
 
 a) Enter Environment Name          : default [partner-eb-meanstack-atlas-dev]
 
 b) Enter DNS CNAME prefix          : default [partner-eb-meanstack-atlas-dev]
 
CNAME should be unique. if it gives an option on account of duplicate, select the default option suggested.

Copy and paste the DNS CNAME selected to the code as the private URL. Location: "client --> src --> app --> employee.service.ts (line 10)"

Ensure the CNAME selected and Private URL server names are the same.

Also ensure the region in the URL to updated to the region selected during eb init.

Refer the below screenshot for further details
 
 c) Select a load balancer type     : default [application]
 
 d) Would you like to enable Spot Fleet requests for this environment? (y/N): default [N]
 
 
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp17.png)
 
 
 e. Ensure the successful creation of the environment. It will take minimum 10mins to create the environment.
 
 <img width="863" alt="image" src="https://user-images.githubusercontent.com/101570105/202484018-6c2acd15-e09f-48a0-a59d-435069a32fb8.png">

 
        
 f. Update the configuration parameters for Loadbalancer in the below sequence (only)
 
  a. update the Processes - deafult : Change the port to 8000
  
  b. Add a new process for the backend with port 5200 and HTTP code to 200,404
  
  c. insert a new listener for the backend process created.
  
 
 ![](https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB/blob/main/images/16.EBcreateasampleapp14.png)
 
 
 g. Ensure the configuration changes are applied successfully
 ![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBcreateasampleapp15.png)


## Step4: Test the application

 The endpoint of the application is displayed in the elastic beanstalk environment. ex: partner-eb-meanstack-atlas-dev2.us-east-1.elasticbeanstalk.com
 
 ![](https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB/blob/main/images/ebfinalpage.png)
 
 
 Test the application for CRUD operations and ensure the data are reflected in MongoDB Atlas documents


![](https://github.com/Babusrinivasan76/ebintegrationwithatlas/blob/main/images/16.EBSMeanstackOutput-1.png)


![](https://github.com/Babusrinivasan76/MEANSTACKwithAtlasonAWSEB/blob/main/images/17.EBSMeanstackupdatedbs-1.png)


## Troubleshoot

Errors: 

a) The current user does not have the correct permissions. Reason: Operation Denied. The security token included in the request is invalid.

b) ebcli.lib.aws : Error while contacting Elastic Beanstalk Service ERROR: ('Connection aborted.', gaierror(-2, 'Name or service not known'))


Steps: 

a) Verify the AWS profile is set.

b) remove the folder .elasticbeanstalk (in partner-eb-meanstack-atlas directory) and restart the steps from begining.




## Summary:

Any containerized application can be deployed within no time using this template. 
Please check out the [Application Modernization with Fargate](https://github.com/mongodb-partners/MEANStack_with_Atlas_on_Fargate) to have similar deployments on AWS Fargate

Pls share your feedback/queries to partners@mongodb.com

 

