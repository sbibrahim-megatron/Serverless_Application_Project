
## Serverless 

![Overview](https://ordina-jworks.github.io/img/2018-10-01-How-to-Build-a-Serverless-Application/AWS-Lambda-and-DynamoDB-Architecture.png)

## Characteristics of Serverless

![Xtics](https://ordina-jworks.github.io/img/2018-10-01-How-to-Build-a-Serverless-Application/AWS-Lambda-and-DynamoDB-Architecture.png)

## Advantages of Serverless

![Advantages-of-Serverless]https://marvel-b1-cdn.bc0a.com/f00000000216283/www.fortinet.com/content/fortinet-com/en_us/resources/cyberglossary/serverless-computing/_jcr_content/par/c05_container_copy_c_1683859126/par/c28_image.img.png/1663262398467.png


The ability to delegate more of your operational duties to AWS  is made easy by using serverless services in the cloud architecture. Adoption of a technology like serverless computing helps enterprises become more efficient and extract maximum potential from existing resources within economical costs. It does away with infrastructure management duties like capacity provisioning, operating system upkeep, server or cluster provisioning, and patching. Almost any backend service or application can be built with them, and everything needed to run and scale your application with high availability is taken care of for you.

## AWS Lambda

![sample-blank](https://digitalcloud.training/wp-content/uploads/2021/11/What-is-AWS-Lambda-768x489.jpg)

![sample-blank](https://k21academy.com/wp-content/uploads/2021/02/AWSLambda_Diagram-04-1024x393.png)

You can run code with AWS Lambda without setting up or managing servers. There is no fee when your code is not executing; you only pay for the compute time you use.

You may use Lambda to run code for almost any kind of application or backend service with no administration required. Simply upload your code, and Lambda will handle all the necessary steps to run and grow it with high availability.


## Amazon API Gateway

![api-gateway](https://user-images.githubusercontent.com/80678596/177031280-4e4b0747-2213-4abf-81fc-8bc46e18b38e.png)


In order to construct, publish, maintain, monitor, and protect APIs at any size, developers can use the fully managed service known as Amazon API Gateway. It provides a complete framework for managing APIs. API Gateway manages traffic, permission and access control, monitoring, and API version management while enabling you to perform hundreds of thousands of API calls concurrently.

## Amazon DynamoDB

<img width="1861" alt="db" src="https://user-images.githubusercontent.com/80678596/177031324-b3bc4476-a2ee-4697-9aeb-76b29345acdf.png">

A consistent, single-digit millisecond latency at any scale is required by all applications, and Amazon DynamoDB provides a quick and adaptable NoSQL database service that can meet this need.

For internet-scale applications, it is a fully managed, multiregion, multimaster, persistent database with built-in backup and restore, security, and in-memory caching.

## Amazon S3

![s3](https://user-images.githubusercontent.com/80678596/177031215-0ad4013e-4111-4f29-a4e4-d916a9b8eec0.png)

Amazon Simple Storage Service is a cloud-based object storage service with industry-leading scalability, data availability, security, and performance. Amazon S3 is a simple web service interface that allows you to store and retrieve any amount of data from anywhere on the internet.

Customers of all sizes and industries can use it to store and protect any amount of data for a variety of use cases, including websites, mobile apps, backup and restore, archiving, enterprise applications, IoT devices, and big data analytics.

# Demo
 ![TODO](images/AddTodo-with-images.PNG)

# Serverless TODO

In this project I develop and deploy a simple "TODO" application using AWS Lambda and Serverless framework. This application will allow users to create/remove/update/get TODO items. Each TODO item contains the following fields: 
   - todoId (string) - a unique id for an item
   - createdAt (string) - date and time when an item was created
   -  name (string) - name of a TODO item (e.g. "Change a light bulb")
   - dueDate (string) - date and time by which an item should be completed
   - done (boolean) - true if an item was completed, false otherwise
   - attachmentUrl (string) (optional) - a URL pointing to an image attached to a TODO item

# Functions implemented

To implement this project you need to implement the following functions and configure them in the `serverless.yml` file:

* `Auth` - this function should implement a custom authorizer for API Gateway that should be added to all other functions.
* `GetTodos` - should return all TODOs for a current user. 
* `CreateTodo` - should create a new TODO for a current user. A shape of data send by a client application to this function can be found in the `CreateTodoRequest.ts` file
* `UpdateTodo` - should update a TODO item created by a current user. A shape of data send by a client application to this function can be found in the `UpdateTodoRequest.ts` file
* `DeleteTodo` - should delete a TODO item created by a current user. Expects an id of a TODO item to remove.
* `GenerateUploadUrl` - returns a presigned url that can be used to upload an attachment file for a TODO item. 

All functions are already connected to appriate events from API gateway

An id of a user can be extracted from a JWT token passed by a client

You also need to add any necessary resources to the `resources` section of the `serverless.yml` file such as DynamoDB table and and S3 bucket.


## Deploy Backend

                  cd backend

                  npm install
  
                  serverless

                  npm install --save-dev serverless-iam-roles-per-function@next 

                  serverless deploy --verbose


# Endpoints
   
  - GET - https://07ep79xqe4.execute-api.us-east-1.amazonaws.com/prod/todos
  - POST - https://07ep79xqe4.execute-api.us-east-1.amazonaws.com/prod/todos
  - PATCH - https://07ep79xqe4.execute-api.us-east-1.amazonaws.com/prod/todos/{todoId}
  - DELETE - https://07ep79xqe4.execute-api.us-east-1.amazonaws.com/prod/todos/{todoId}
  - POST - https://07ep79xqe4.execute-api.us-east-1.amazonaws.com/prod/todos/{todoId}/attachment

functions:
  
# Lambda Functions

  - Auth: serverless-demegatron-prod-Auth
  - GetTodos: serverless-demegatron-prod-GetTodos
  - CreateTodo: serverless-demegatron-prod-CreateTodo
  - UpdateTodo: serverless-demegatron-prod-UpdateTodo
  - DeleteTodo: serverless-demegatron-prod-DeleteTodo
  -  GenerateUploadUrl: serverless-demegatron-prod-GenerateUploadUrl 
  
# Serverless 

[label1](images/Serverless%20Dashboard.PNGC:/Users/i84202155/Desktop/Serverless_Application_Project/README.md)
  
  
  
# Auth0

  ![Auth01](https://user-images.githubusercontent.com/120554885/221633829-8c2f86e3-d4c4-47e0-a6cf-9a4c9915467a.jpg)

# AWS Cloud Formation 

<img width="813" alt="AWS_CloudFormation" src="https://user-images.githubusercontent.com/120554885/221633959-28f81b41-3f20-4058-9eee-f2e474910bb6.PNG">

   

# Frontend

The `client` folder contains a web application that can use the API that should be developed in the project.

To use it please edit the `config.ts` file in the `client` folder:

```ts
const apiId = '...' API Gateway id
export const apiEndpoint = `https://${apiId}.execute-api.us-east-1.amazonaws.com/prod`

export const authConfig = {
  domain: '...',    // Domain from Auth0
  clientId: '...',  // Client id from an Auth0 application
  callbackUrl: 'http://localhost:3000/callback'
}
```


# Suggestions

To store TODO items you might want to use a DynamoDB table with local secondary index(es). A create a local secondary index you need to a create a DynamoDB resource like this:

```yml

TodosTable:
  Type: AWS::DynamoDB::Table
  Properties:
    AttributeDefinitions:
      - AttributeName: partitionKey
        AttributeType: S
      - AttributeName: sortKey
        AttributeType: S
      - AttributeName: indexKey
        AttributeType: S
    KeySchema:
      - AttributeName: partitionKey
        KeyType: HASH
      - AttributeName: sortKey
        KeyType: RANGE
    BillingMode: PAY_PER_REQUEST
    TableName: ${self:provider.environment.TODOS_TABLE}
    LocalSecondaryIndexes:
      - IndexName: ${self:provider.environment.INDEX_NAME}
        KeySchema:
          - AttributeName: partitionKey
            KeyType: HASH
          - AttributeName: indexKey
            KeyType: RANGE
        Projection:
          ProjectionType: ALL # What attributes will be copied to an index

```

To query an index you need to use the `query()` method like:

```ts
await this.dynamoDBClient
  .query({
    TableName: 'table-name',
    IndexName: 'index-name',
    KeyConditionExpression: 'paritionKey = :paritionKey',
    ExpressionAttributeValues: {
      ':paritionKey': partitionKeyValue
    }
  })
  .promise()
```


## Deploy Frontend

To run a client application first edit the `client/src/config.ts` file to set correct parameters. And then run the following commands

```
cd client
npm install
npm run start
```

### Working Todo

<img width="960" alt="AddTodo-with-images" src="https://user-images.githubusercontent.com/120554885/221634122-36dc29fb-7154-4ddc-8ade-fa2e672242a0.PNG">

### Blank Todo 

<img width="960" alt="Failed_running_blankTodo" src="https://user-images.githubusercontent.com/120554885/221634236-a3fefd33-5e1a-4f82-b5e6-917860340f4e.PNG">



This should start a development server with the React application that will interact with the serverless TODO application.
