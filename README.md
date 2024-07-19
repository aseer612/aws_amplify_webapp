# Wild Rydes Serverless Application

## Overview
This project is a serverless web application hosted on AWS using AWS Amplify. It includes user authentication through AWS Cognito, ride data management with DynamoDB, and API management with API Gateway and Lambda functions.

## Architecture
The architecture of this project includes the following components:
1. **Frontend**: Hosted on AWS Amplify, integrated with a Git repository for CI/CD.
2. **Authentication**: AWS Cognito is used to handle user authentication and authorization.
3. **API Gateway**: Acts as the entry point for API requests and integrates with Lambda functions.
4. **Lambda Functions**: Used to process requests and interact with DynamoDB.
5. **DynamoDB**: A NoSQL database used to store ride request data.
6. **IAM**: Roles and policies to manage permissions securely.

![Architecture Diagram](path/to/your/architecture-diagram.png)

### Detailed Architecture Components
- **AWS Amplify**: Hosts the static files of the frontend application. It also handles continuous integration and deployment from a Git repository.
- **AWS Cognito**: Provides user pool and identity pool to handle user registration, authentication, and authorization.
- **Amazon API Gateway**: Acts as a front door to handle all the API requests from the frontend. It integrates with Lambda functions to handle the backend logic.
- **AWS Lambda**: Contains the serverless functions that perform business logic and interact with DynamoDB. Functions are triggered by API Gateway events.
- **Amazon DynamoDB**: Stores the ride request data with a schema-less architecture, allowing for flexible and scalable data storage.
- **AWS IAM**: Manages roles and policies to ensure least privilege access to AWS resources, enhancing security.

## Setup Instructions

### Prerequisites
- AWS Account
- AWS CLI configured with necessary permissions
- Node.js installed
- Git installed

### Step 1: Create a Repository
Create a repository where all the codes will be saved it could be GitHub or codecommmit
for this project we will be using GitHub

### Step 2: Set Up the Frontend (using AWS amplify)
-Select GitHub as the repository source.
-Authenticate with GitHub and select the appropriate repository.
-Keep other settings as default and proceed to deploy application

### Step 3: Set Up Cognito
1. Create a new Cognito user pool:
  - Navigate to the Cognito console.
  - Click Create user pool.
  - Configure the pool with the preferred sign-in option (e.g., email).
  - Disable MFA for simplicity and proceed with default settings.
  - Use Cognito's default email service for sending verification emails.
  - Name your user pool and app client.
2. Update application configuration:
  - Note down the User Pool ID and App Client ID.
  - Update in repo src/js/config.js with these values

![Cognito id update](https://github.com/user-attachments/assets/f979bfec-f524-455f-96cc-0f8548075f55)


### Step 4: Set Up DynamoDB
- Create a new DynamoDB table:
Navigate to the DynamoDB console.
  - Click Create table.
  - Name the table Rides.
  - Set the partition key as RideId (String).
  - Copy the table ARN: You will need this ARN for configuring IAM policies.
 
### Step 5: Set Up IAM Roles
- Create a new IAM role for Lambda:
Navigate to the IAM console.
  -Click Roles > Create role.
  -Select Lambda as the service.
  -Attach the AWSLambdaBasicExecutionRole policy.
  -Complete the role creation process.
  -Add an inline policy to the role:

- Go back to the IAM role you created.
  -Click Add inline policy.
  -Select DynamoDB as the service.
  -Allow the action dynamodb:PutItem.
  -Add the ARN of the DynamoDB table.
  -Name and create the policy.

### Step 6: Create Lambda Functions
1. Create a new Lambda function:
Navigate to the Lambda console.
  -Click Create function.
  -Choose Author from scratch.
  -Name the function and set the runtime to Node.js 16.x.
  -Change the execution role to the one created earlier.
2. Deploy the Lambda function code:
  - Replace the contents of index.js with the provided code in src section file name <index.js>
  - create a test case using code stored in src section file name <lambda-test>

### Step 7: Set Up API Gateway
1. Create a new REST API:
Navigate to the API Gateway console.
  - Click Create API > REST API > Build.
  - Name the API and select Edge-optimized as the endpoint type.
    
2. Add a Cognito authorizer:
Go to the Authorizers tab.
  -Click Create New Authorizer.
  -Name the authorizer and select the Cognito user pool.
  -Set the token source to Authorization.3
   
4. Create a new resource and method:
Go to the Resources tab.
  -Click Create Resource and name it ride.
  -Select the ride resource and click Create Method.
  -Select POST and integrate with the Lambda function.
  -Enable Lambda proxy integration.
   
6. Deploy the API:
Go to the Deployments tab.
  -Create a new deployment stage (e.g., dev).
  -Copy the invoke URL and update src/js/config.js:

wait for amplify to deploy changes and start ordering the unicorn



