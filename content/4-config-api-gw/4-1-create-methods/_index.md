---
title : "Create methods"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
#### Create list API
1. Click **/books**, then select **Create method**
![CreateListAPI](/images/1/44.png?width=90pc)

2. In the Method detail
    - Select **GET** method
    -  Select **Lambda Function** for **Integration type**
    - Check to **Use Lambda Proxy integration**
    - Enter Lambda function name to be integrated: **books_list**
    - Click **Save**
![CreateListAPI](/images/1/45.png?width=90pc)
3. Click **Create method**
![CreateListAPI](/images/1/46.png?width=90pc)
#### Create write API
1. Click **/books**, then select **Create method**
![CreateListAPI](/images/1/47.png?width=90pc)
2. In the Method detail
    - Select **GET** method
    -  Select **Lambda Function** for **Integration type**
    - Check to **Use Lambda Proxy integration**
    - Enter Lambda function name to be integrated: **books_list**
    - Click **Save**
![CreateListAPI](/images/1/48.png?width=90pc)
3. Click **Create method**
![CreateListAPI](/images/1/49.png?width=90pc)

#### Create delete API
1. Click **/books**, then select **Create Resource**
![CreateListAPI](/images/1/50.png?width=90pc)
2. For **Create Resource**
    - Enter **{id}** for **Resource name** pattern
    - Click **Create Resource**
![CreateListAPI](/images/1/51.png?width=90pc)
3. Click **/{id}**, then select **Create method**
![CreateListAPI](/images/1/52.png?width=90pc)


4. For **Method detail** 
    - Select method **DELETE**
    - Select **Lambda Function** for **Integration type**
    - Check to **Use Lambda Proxy integration**
    - Enter Lambda function name to be integrated: **book_delete**
    - Click **Save**
![CreateListAPI](/images/1/53.png?width=90pc)
5. Click **Create method**
![CreateListAPI](/images/1/54.png?width=90pc)
So, we have created the APIs that interact with Lambda functions.