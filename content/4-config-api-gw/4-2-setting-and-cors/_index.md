---
title : "Setting and enable CORS"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

In this section, we will add binary file support settings and enable CORS for the APIs.

1. Go to **API Settings** page.
    - Click **API Settings** on the left menu.
    - Click **Manage media types**.
      ![CreateRestAPI](/images/temp/1/65.png?width=90pc)

2. At **Manage binary media types** page.
    - Click **Add binary media type**.
    - Enter `multipart/form-data`.
    - Click **Save Changes**.
      ![CreateRestAPI](/images/temp/1/66.png?width=90pc)

3. Back to **Resource** page.
    - Click **Resources**.
    - Select **/books** resource.
    - Select **Enable CORS**.
      ![CreateRestAPI](/images/temp/1/67.png?width=90pc)

4. At **Enable CORS** page.
    - Choose **GET** and **POST** for **Access-Control-Allow-Methods**.
    - Leave as default and click **Save**.
      ![CreateRestAPI](/images/temp/1/68.png?width=90pc)

5. At **Resources** page.
    - Click **Resources**.
    - Select **/{id}** resource.
    - Select **Enable CORS**.
      ![CreateRestAPI](/images/temp/1/69.png?width=90pc)

6. At **Enable CORS** page.
    - Choose **DELETE** for **Access-Control-Allow-Methods**.
    - Leave as default and click **Save**.
      ![CreateRestAPI](/images/temp/1/70.png?width=90pc)

7. To front-end can use APIs, we need deploy APIs. Back to **Resources** page.
    - Click **Resources**.
    - Select **/** resource.
    - Click **Deploy API**.
      ![CreateRestAPI](/images/temp/1/71.png?width=90pc)

8. At **Deploy API** modal.
    - Select **New stage**.
      ![CreateRestAPI](/images/temp/1/72.png?width=90pc)
    - Enter stage name, such as: `staging`.
    - Click **Deploy**.
      ![CreateRestAPI](/images/temp/1/73.png?width=90pc)

9. Take note URL to call API. Go to **Stages** page.
    - Click **Stages**.
      ![CreateRestAPI](/images/temp/1/74.png?width=90pc)
    - URL of **list** and **write** API:
      ![CreateRestAPI](/images/temp/1/75.png?width=90pc)
    - URL of **delete** API:
      ![CreateRestAPI](/images/temp/1/76.png?width=90pc)
