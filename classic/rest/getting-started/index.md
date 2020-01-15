---
template: page-sidebar
title: "Optimizely REST API Guide"
---

# Getting started with Optimizely's REST API

Get started with the REST API in 5 minutes by following the instructions below:

### 1. Log in to your Optimizely account

Log in at <a href="https://app.optimizely.com/signin" target="_blank">https://app.optimizely.com/signin</a>.

### 2. Generate an API token

Visit <a target="_blank" href="https://app.optimizely.com/tokens">app.optimizely.com/tokens</a> to generate a API token, which you'll need to authenticate with the API.

*Note:* If you didn't create your own account, you'll need to make sure you have Administrator or Project Owner permissions to generate a token. If you don't have permissions, ask your Administrator or Project Owner to generate a token for you.

### 3. Access your account

To use the REST API, you'll need to include your API token in the request header. For example, the following request returns a list of projects in your account.

```curl
curl \
  -H "Token: abcdefghijklmnopqrstuvwxyz:123456" \
  -X GET "https://www.optimizelyapis.com/experiment/v1/projects/"
```

### 4. Register your application

Register your application in your [account settings](http://app.optimizely.com/accountsettings/developer).

If you're developing an application for use by other customers, we recommend registering your application so you can use OAuth 2.0 to authenticate with the API. OAuth 2.0 will allow customers to use your application without requiring them to share their Optimizely username and password. For more information on how to use OAuth, refer to our [OAuth documentation](/rest/reference#oauth).

### 5. Start building!

You're now ready to start building an application with Optimizely! Please refer to our full [API reference](/rest/reference) to see a full list of the supported endpoints. 

If you have any questions about using the REST API, you can [submit a ticket to the developer support team](https://optimizely.com/support). We'll be happy to help as you build your application.
