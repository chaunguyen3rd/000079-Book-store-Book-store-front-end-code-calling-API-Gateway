---
title : "Config API Gateway"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
Next, we'll set up the API Gateway to interact with the Lambda functions created in the previous section:

1. Open [API Gateway console](https://ap-southeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-southeast-2).
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/50.png?width=90pc)

2. Scroll down and click **Build** of **REST API** pattern.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/51.png?width=90pc)

3. At **Create REST API** page.
    - Select **New API** to create a new API.
    - Enter REST API name, such as: **fcj-serverless-api**.
    - For **API endpoint type**, choose **Regional**.
    - Click **Create API**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/52.png?width=90pc)

4. At **Resources - fcj-serverless-api** page.
    - Click **Create resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/53.png?width=90pc)

5. At **Create resource** page.
    - Enter resource name, such as: **books**.
    - Then click **Create Resource**.
![CreateRestAPI](/000079-Book-store-Book-store-front-end-code-calling-API-Gateway/images/temp/1/54.png?width=90pc)

So we have created a new REST API and resource for it. Next, we will create methods to interact with Lambda functions and set them:
1. [Create methods](4-1-create-methods/)
2. [Setting and enable CORS](4-2-setting-and-cors/)

