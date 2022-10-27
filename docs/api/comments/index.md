---
layout: default
title: Comments
parent: API
---

# API for Comments

This page describes how to retreive all comments for a document, post a new
comment, update it and then remove it.

| Action | Endpoint | Description |
| ------ | -------- | ----------- |
| `GET`    | `/API/Comment/{documentId}` | Get all comments for `documentId` |
| `POST`   | `/API/Comment/{documentId}` | Post a comment to `documentId` |
| `PATCH`  | `/API/Comment/{commentId}` | Update comment `commentId` |
| `DELETE` | `/API/Comment/{commentId}` | Delete comment `commentId` |


{: .note }
> We assume that the user is authenticated, either with a JWT token or with 
> a Cookie, for example when using the Swagger interface. For the examples, 
> we assume that the application is running on `http://localhost:5001`.

## Get all comments for a document

To retreive all comments associated with the document `$DOCUMENT_ID`, we
can emit the following request

```
curl -X 'GET' \
  'http://localhost:5001/API/Comment/$DOCUMENT_ID' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

At the moment, this will return an empty list.

```
[]
```

Indeed, this will return the comments associated with the document (none at
moment). For example, after the next section where we posted a comment, the
call above would return

```
[
  {
    "commentId": "723cc24c-739e-4b9a-a36e-a476aec206db",
    "commentDate": "2022-10-25T22:36:58.827394",
    "modificationDate": "2022-10-25T22:36:58.827394",
    "body": "<p>This is a short <b>Bold</b> comment</p>",
    "author": {
      "userId": "26e88626-fa52-4e6a-945b-e6b0c9a54a9d",
      "userName": "ancailliau",
      "email": "antoine@example.org",
      "firstName": "Antoine",
      "lastName": "Cailliau",
      "function": "Data Hoarder of its Majesty",
      "lastActivity": "0001-01-01T00:00:00",
      "registrationDate": "2022-09-19T19:12:54.770609",
      "enabled": true,
      "friendlyName": "Antoine Cailliau"
    },
    "lastModifiedBy": {
      "userId": "26e88626-fa52-4e6a-945b-e6b0c9a54a9d",
      "userName": "ancailliau",
      "email": "antoine@example.org",
      "firstName": "Antoine",
      "lastName": "Cailliau",
      "function": "Data Hoarder of its Majesty",
      "lastActivity": "0001-01-01T00:00:00",
      "registrationDate": "2022-09-19T19:12:54.770609",
      "enabled": true,
      "friendlyName": "Antoine Cailliau"
    }
  }
]
```

## Post a new comment

To post a new comment, the body of the comment is to be encoded in a JSON
object with a property `body`. Body are HTML string that will sanitized by
the application, just like in the web application. For example, the following 
is a perfectly valid comment.

```
{
  "body": "<p>This is a short <b>Bold</b> comment</p>"
}
```

That comment can be posted to a specific document with the following `curl`
command. We assume that `$DOCUMENT_ID` matches the document identifier you want
to post the comment to.

```
curl -X 'POST' \
  'http://localhost:5001/API/Comment/$DOCUMENT_ID' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "body": "<p>This is a short <b>Bold</b> comment</p>"
}'
```

The command above will return the comment as recorded by DocIntel. 

```
{
  "commentId": "723cc24c-739e-4b9a-a36e-a476aec206db",
  "commentDate": "2022-10-25T22:36:58.827394+02:00",
  "modificationDate": "2022-10-25T22:36:58.827394+02:00",
  "body": "<p>This is a short <b>Bold</b> comment</p>",
  "author": {
    "userId": "26e88626-fa52-4e6a-945b-e6b0c9a54a9d",
    "userName": "ancailliau",
    "email": "antoine@example.org",
    "firstName": "Antoine",
    "lastName": "Cailliau",
    "function": "Data Hoarder of its Majesty",
    "lastActivity": "0001-01-01T00:00:00",
    "registrationDate": "2022-09-19T19:12:54.770609",
    "enabled": true,
    "friendlyName": "Antoine Cailliau"
  },
  "lastModifiedBy": {
    "userId": "26e88626-fa52-4e6a-945b-e6b0c9a54a9d",
    "userName": "ancailliau",
    "email": "antoine@example.org",
    "firstName": "Antoine",
    "lastName": "Cailliau",
    "function": "Data Hoarder of its Majesty",
    "lastActivity": "0001-01-01T00:00:00",
    "registrationDate": "2022-09-19T19:12:54.770609",
    "enabled": true,
    "friendlyName": "Antoine Cailliau"
  }
}
```

As we can see in the web application, our comment was posted.

![](/docs/api/assets/imgs/post-comment.png){:.screenshot}

## Edit a comment

If we wish to update the comment created in previous section, we need to send a
`PATCH` request with the `commentId` provided above. The format for providing
the body is the same as above, for posting a new comment. For example,

```
{
  "body": "<p>This is a short <b>Bold</b> comment</p>"
}
```

That can be submited to update the comment. Note that
`723cc24c-739e-4b9a-a36e-a476aec206db` is the identifier provided in the
response property `commentId` in the section above.

```
curl -X 'PATCH' \
  'http://localhost:5001/API/Comment/723cc24c-739e-4b9a-a36e-a476aec206db' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "body": "<p>This is a less strong comment</p>"
}'
```

Again, we receive the comment as recorded. The web application of course
reflect our changes.

![](/docs/api/assets/imgs/update-comment.png){:.screenshot}

## Delete a comment

To delete a comment, we simply send a `DELETE` request with the same identifier
we used to update the comment.

```
curl -X 'DELETE' \
  'http://localhost:5001/API/Comment/723cc24c-739e-4b9a-a36e-a476aec206db' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

This returns an empty `200` response. The comment is now gone from our 
web application interface.