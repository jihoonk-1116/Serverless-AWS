# Serverless-AWS

Key Features and Benefits of Serverless

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

#1. Integrate API Gateway with Lambda

