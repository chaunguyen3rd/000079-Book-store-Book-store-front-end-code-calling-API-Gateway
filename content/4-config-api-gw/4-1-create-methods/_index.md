---
title : "Create methods"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
#### Create list API
1. At **Resource** page.
    - Click **/books**, then select **Create method**.
![CreateRestAPI](/images/temp/1/55.png?width=90pc)

2. At **Create method** page.
    - Select **GET** method.
    - Select **Lambda function** for **Integration type**.
    - Enable **Lambda proxy integration**.
    - Enter Lambda function name to be integrated: **books_list**.
  ![CreateRestAPI](/images/temp/1/56.png?width=90pc)
    - Scroll down to the bottom and click **Create method**.
  ![CreateRestAPI](/images/temp/1/57.png?width=90pc)

#### Create write API
1. At **Resource** page.
    - Click **/books**, then select **Create method**.
![CreateRestAPI](/images/temp/1/55.png?width=90pc)

2. At **Create method** page.
    - Select **POST** method.
    - Select **Lambda function** for **Integration type**.
    - Enable **Lambda proxy integration**.
    - Enter Lambda function name to be integrated: **book_create**.
  ![CreateRestAPI](/images/temp/1/58.png?width=90pc)
    - Scroll down to the bottom and click **Create method**.
  ![CreateRestAPI](/images/temp/1/59.png?width=90pc)

#### Create delete API
1. At **Resource** page.
    - Click **/books**, then click **Create resource**.
![CreateRestAPI](/images/temp/1/60.png?width=90pc)

2. At **Create resource** page.
    - Enter **{id}** for **Resource name** pattern.
    - Click **Create Resource**.
![CreateRestAPI](/images/temp/1/61.png?width=90pc)

3. At **Resource** page.
    - Click **/{id}**.
    - Select **Create method**.
![CreateRestAPI](/images/temp/1/62.png?width=90pc)

4. At **Create method** page.
    - Select **DELETE** method.
    - Select **Lambda function** for **Integration type**.
    - Enable **Lambda proxy integration**.
    - Enter Lambda function name to be integrated: **book_delete**.
  ![CreateRestAPI](/images/temp/1/63.png?width=90pc)
    - Scroll down to the bottom and click **Create method**.
  ![CreateRestAPI](/images/temp/1/64.png?width=90pc)

So, we have created the APIs that interact with Lambda functions.