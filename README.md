# Serverless-TODO APP Backend with AWS Lambda

# Language & Tools
 * Nodejs
 * Lambda
 * API Gateway
 * Serverless Framework
 * CodeCommit, CodeBuild for CI/CD with buildspec.yml
 * DynamoDB
 * Postman

# CRUD API 
All API should include the headers: <br>
![image](https://user-images.githubusercontent.com/76544061/178170234-41a43882-dfd8-406f-a00e-257cef61a870.png) <br>

## Get all todos
- https://t1wg3lq3v1.execute-api.us-east-1.amazonaws.com/prod/notes
- Response : <br>
<img src="https://user-images.githubusercontent.com/76544061/178170275-44f6e89a-fcf6-4853-bc85-7320c5205a0a.png" width="800"/>


## Post todo
- https://t1wg3lq3v1.execute-api.us-east-1.amazonaws.com/prod/note
- Request & Response : <br>
<img src="https://user-images.githubusercontent.com/76544061/178170421-62465730-15d3-4dd2-ac1c-aed0f6a7680b.png" width="700"/>

## Update todo
- https://t1wg3lq3v1.execute-api.us-east-1.amazonaws.com/prod/note
- Request & Response : <br>
<img src="https://user-images.githubusercontent.com/76544061/178170482-c33b1395-f24f-469a-aba0-ee59dc1e87f1.png" width="700"/>

## Delete todo
- https://t1wg3lq3v1.execute-api.us-east-1.amazonaws.com/prod/note/t/{note_id}
- Before Request : <br>
<img src="https://user-images.githubusercontent.com/76544061/178170611-30ccc607-2c3b-4c1f-be49-8f04ae80b3cd.png" width="700"/>
- Delete Request : <br>
<img src="https://user-images.githubusercontent.com/76544061/178170670-5231264d-1e6c-4814-91b5-ff203afb6989.png" width="700"/>
- After Request: <br>
<img src="https://user-images.githubusercontent.com/76544061/178170689-4f040204-a160-47dd-95ab-4bc301045ac7.png" width="700"/>


# CI/CD Flow
 CodeCommit -> push trigger -> Code Build -> Operate following buildspec.yml -> Initiate deploying by Serverless Framework using serverless.yml
 -> Set up Lambda, API Gateway, DynamoDB -> Complete...<br>
 
## Code PipeLine
![image](https://user-images.githubusercontent.com/76544061/178172381-0230fd75-9c50-493f-9f05-ca5ec1a25a99.png)

## Code Build
![image](https://user-images.githubusercontent.com/76544061/178172584-e7c79410-2077-490d-8556-0cb8fe67709f.png)
![image](https://user-images.githubusercontent.com/76544061/178172670-8485cf74-2118-40ad-bfe5-970f1aecab1f.png)


# Key Features and Benefits of Serverless


  * No server management
  * Easy & Efficient Scaling
  * Built in High Availability and Fault Tolerance
  * Service Integration
  * No idle capacity
  
Challenges with serverless architecture
  * Vendor Lock-ins
  * Public Cloud
  * Level of Control
  
Core Serverless Services 
  * Lambda
  * API Gateway
  * DynamoDB
  
# Lambda
## Two Arguments
1. Event
  - Input data or input parameters
  - It depends on event source
  - Invocation Type 
    * Async - S3
    * Sync - API Gateway, Cognito
  - Event sources type
    * Push event - S3, API Gateway
    * Pull event (Lambda poll event stream to look for event data) - DynamoDB, Kinesis, SQS

2. Context
  Lambda functions environment - name, remaining time, allocated memory size, request info
  
  
  
# DynamoDB
 - Serverless, Cloud, NoSQL, Fast, Flexible, Cost Effective, Highly Scalable, Fault Tolerant, Secure
 
 ![image](https://user-images.githubusercontent.com/76544061/177243986-49c5cc65-75ef-45f9-8fd5-aeb31fdd99a9.png)
 
 ![image](https://user-images.githubusercontent.com/76544061/177244106-5087449c-bb97-49a3-af46-0874d94f1bd5.png)

## Data Types
 - Scalar Types : Exactly one value(String, num, boolean, null)
 - Set Types : Multiple scalar values (String set, num set)
 - Document Types : Complex Structure with nested attributes (list, map)

## Consistency Model
Automatic Synchronous Replication - 3 Facilities
 - High Availability
 - 3 copies of data within a region
 - Act as independent Failure Domains
 - Near Real-time Replication
 
Read Consistency
 - Strong Consistency
   * The most up-to-date data
   * Must be requested explicitly
   
 - Eventual Consistency
   * May or may not reflet the latest copy of data
   * Default consistency for all operations
   * 50% cheaper
   
DynamoDB Capacity & pricing
 - Tables 
   * Top-Level entities
   * No strict inter-table relationships
   * Mandatory primary keys
   * Control performance at the table level
 - Throughput Capacity
   * Allows for predictable performance at scale
   * Used to control read/write throughput
   * Supports auto-scaling
   * Defined using RCUs and WCUs
   * Major factor in DynamoDB pricing
   * 1 capacity unit = 1 request/sec
   
   ![image](https://user-images.githubusercontent.com/76544061/177246402-3be07120-d742-4554-b76c-990409a9a959.png)
![image](https://user-images.githubusercontent.com/76544061/177246548-c15360b9-2811-4099-b142-c88235a517b7.png)

DynamoDB Partitions
  - Store DynamoDB table data
  - A table can have multiple partitions
  - Number of table partitions depend on its size and provisioned capacity
  - Managed internally by DynamoDB
  - 1 partition = 10GB of data
  - 1 partition = 1000 WCUs or 3000 RCUs

![image](https://user-images.githubusercontent.com/76544061/177247185-3463b22b-d4dd-41a3-9704-49f82579cc24.png)


Indexes 
 - Primary Index (Table index)
 - Secondary Index - Local, Global
   * Local Index has be assigned when initiating a table 
   * Global index can be made any time - Only eventually consistent reads
   * 5 local & global secondary indexes per table
 - Index Key 
    * Simple Key : Only Partition Key
    * Composite Key : Partition Key + Sort Key
 - Partition or Hash Key decides the target partition

# More about Lambda 
  Getting function name, version
  
  exports.handler = async (event, context) => {
    let log = event;
    
    log.lambdaFunction = context.functionName;
    log.lambdaFunction = context.functionVersion;
    
    return log;
  }
  
 - $LATEST indicates latest verion
 
 Lambda Alias 
  - An alias is a pointer to one or two versions
  - Using Aliases and stage variables, we no longer have to re-deploy the API when we change the backed Lambda function
  - Alias : dev, prod, test
 Traffic shifting
  - Lambda will automatically split the incoming request traffic as per our split settings
 Canary deployment 
  - is used to test new API deployments and change to stage variables 
 Environment variables
  - Key-value pairs that are accessble from function code
  - useful to store configuration settings without the need to change function code
  - ex) APP_NAME : My App 
  - In code, it can be acessed process.env.APP_NAME
 Encryption Environment Variables with KMS
  
  
# Step Functions
 Step Functions are the logical progression of AWS Lambda functions
  - visual work flow to coordinate or orchestrate Lambda functions to work together
  - automate routine jobs like deployments, upgrades, migrations, patches
  - build serverless or microservice
  - ASL (Amazon States Language) : define different states or steps of the workflow, connections
  - resulting workflow : state machine

 State Machine
  - StartAt is the required field that must be present in the state machine definition
  - States : Fail, Choice, Parallel

# Example: Resize Image Processor
  Take only a jpg file and resize it 
  
  - Skeleton ASL
  ```
   {
  "Comment": "Image Processor",
  "StartAt": "GetFileType",
  "States": {
    "GetFileType": {
      "Type": "Pass",
      "Next": "CheckFileType"
    },
    "CheckFileType": {
      "Type": "Choice",
      "Choices":[
        {
          "Variable": "$.results.fileType",
          "StringEquals":"jpg",
          "Next":"ProcessFile"
        }
      ],
      "Default":"DeleteSourceFile"
    },
    "DeleteSourceFile":{
      "Type": "Pass",
      "End": true
    },
    "ProcessFile":{
      "Type": "Parallel",
      "Next": "WriteToDynamoDB",
      "Branches":[
        {
          "StartAt":"CopyToDestination",
          "States":{
            "CopyToDestination":{
              "Type":"Pass",
              "End":true
            }
          }
        },
        {
          "StartAt":"ResizeImage",
          "States":{
            "ResizeImage":{
              "Type":"Pass",
              "End":true
            }
          }
        }
      ]
    },
    "WriteToDynamoDB":{
      "Type":"Pass",
      "Next":"DeleteSourceFile"
    }
  }
}
```

## Skeleton Test

Test Input <br>
<img width="328" alt="Screen Shot 2022-07-07 at 11 29 11 PM" src="https://user-images.githubusercontent.com/76544061/177911375-5e2c4ecb-5f3c-496a-a2c8-282c16a79669.png">

<img width="268" alt="Screen Shot 2022-07-07 at 11 27 15 PM" src="https://user-images.githubusercontent.com/76544061/177911270-59488c5e-c1c4-4aa3-8f1e-07f6fe85e1a6.png">
