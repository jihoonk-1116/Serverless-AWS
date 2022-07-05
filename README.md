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

#1. Integrate API Gateway with Lambda

