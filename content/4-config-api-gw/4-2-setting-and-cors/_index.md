---
title : "Setting and enable CORS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---
In this section, we will add binary file support settings and enable CORS for the APIs
1. Select **API Settings** on the left menu.
    - Click **Manage media types**
![CreateRestAPI](/images/1/55.png?width=90pc)

2. Click **Add binary media type**
    - Enter **multipart/form-data**
    - Click **Save Changes**
![CreateRestAPI](/images/1/56.png?width=90pc)

3. After the setting is done, back to **Resource** on the left menu.
    - Select **/books** resource
    - Select **Enable CORS**
![CreateRestAPI](/images/1/57.png?width=90pc)
5. For **Enable CORS**
    - Choose **GET** and **POST** method
    - Click **Save**
![CreateRestAPI](/images/1/58.png?width=90pc)
6. Select **/{id}** resource
    - Select **Enable CORS**
![CreateRestAPI](/images/1/59.png?width=90pc)
7. For **Enable CORS**
    - Choose **DELETE** method
    - Click **Save**
![CreateRestAPI](/images/1/60.png?width=90pc)

9. To front-end can use APIs, we need deploy APIs.
    - Select **/** resource
    - Click **Deploy API**
![CreateRestAPI](/images/1/61.png?width=90pc)

10. Select **New stage**
![CreateRestAPI](/images/1/62.png?width=90pc)

11. Enter stage name, such as: **staging**
    - Click **Deploy**
![CreateRestAPI](/images/1/63.png?width=90pc)

12. Take note URL to call API
![CreateRestAPI](/images/1/64.png?width=90pc)

    - URL of list and write API:
![CreateRestAPI](/images/1/65.png?width=90pc)

    - URL of delete API:
![CreateRestAPI](/images/1/67.png?width=90pc)