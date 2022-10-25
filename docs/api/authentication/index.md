---
layout: default
title: Authentication
parent: API
---

In order to use the API, the user needs to be authenticated. DocIntel supports
two type of authentication for its API. The user can be logged in with cookies,
like when he is using the Web Application. This scenario is very useful when
playing with the Swagger inteface to try the API. The user can also be using a
API key, for example in a script. The API key can then be used to generate a
token that can be used in the session to authenticate the user.

## Create new API key

1. Click on the user profile picture on the top-right of the screen. 
2. Click *Manage API Keys* in the dropdown menu.
3. Click on the button *Create new API key*.
4. Fill the form with a name and a description for your application.
5. Click save.
6. You can now copy/paste and use the API key.

## Usage

To use the API, the user needs to first login to obtain a token. The token can
then be used to authenticate the API calls. To obtain the token, the user
needs to make a `POST` request to `/API/Authentication/Login` endpoint with 
the following body:

```
{
  "username": "MY_USERNAME",
  "apiKey": "MY_API_KEY"
}
```

That will return a JSON document with a single field `token` containing the
token.

For example, executing the following command in a Terminal will result in a token.

```
$ curl -X 'POST' \
  'http://MY_INSTANCE_URL/API/Authentication/Login' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -d '{
  "username": "MY_USERNAME",
  "apiKey": "MY_API_KEY"
}'
{
  "token": "MY_TOKEN"
}
```

With the token, the user can execute API calls. For example

```
curl -X 'GET' \
  'http://MY_INSTANCE_URL/API/Document/Pending?page=1&pageSize=20' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer MY_TOKEN'
```