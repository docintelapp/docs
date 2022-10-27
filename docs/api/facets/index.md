---
layout: default
title: Facets
parent: API
---

# API for Facets

This page describes how to retreive all facets, create, update, merge and delete
facets but as well how users can subscribe to facets.

| Action | Endpoint | Description |
| ------ | -------- | ----------- |
| `GET` | `/API/Facet` | Get all facets |
| `POST` | `/API/Facet` | Create a new facet |
| `GET` | `/API/Facet/{facetId}` | Get facet `facetId` |
| `PATCH` | `/API/Facet/{facetId}` | Update facet `facetId` |
| `DELETE` | `/API/Facet/{facetId}` | Delete facet `facetId` |
| `GET` | `/API/Facet/{facetId}/Subscription` | Get subscription for `facetId` |
| `POST` | `/API/Facet/{facetId}/Subscribe` | Subscribe to `facetId` |
| `POST` | `/API/Facet/{facetId}/Unsubscribe` | Unsubscribe from `facetId` |
| `POST` | `/API/Facet/{primaryId}/Merge/{secondaryId}` | Merge facet `primaryId` with `secondaryId` |

{: .note }
> We assume that the user is authenticated, either with a JWT token or with 
> a Cookie, for example when using the Swagger interface. For the examples, 
> we assume that the application is running on `http://localhost:5001`.

## Get all facets

To retreive all facets known by DocIntel, 

```
curl -X 'GET' \
  'http://localhost:5001/API/Facet' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

It then returns all facets (output is truncated for the documentation
convenience).

```
[
  {
    "facetId": "666d3ecd-35b3-47ac-823a-dd8a95ecb81d",
    "title": "Technique (Defense Evasion)",
    "prefix": "technique.defenseEvasion",
    "description": "<p>The adversary is trying to avoid being detected.</p>\n<p>Defense Evasion consists of techniques that adversaries use to avoid detection throughout their compromise. Techniques used for defense evasion include uninstalling/disabling security software or obfuscating/encrypting data and scripts. Adversaries also leverage and abuse trusted processes to hide and masquerade their malware. Other tactics’ techniques are cross-listed here when those techniques include the added benefit of subverting defenses.</p>\n",
    "mandatory": false,
    "hidden": false,
    "creationDate": "2022-09-19T19:34:52.460488",
    "modificationDate": "2022-09-19T19:34:52.460488",
    "autoExtract": true,
    "tagNormalization": ""
  },
  {
    "facetId": "72af578f-7274-4d39-8910-4f4d2137dfe6",
    "title": "Technique (Privilege Escalation)",
    "prefix": "technique.privilegeEscalation",
    "description": "<p>The adversary is trying to gain higher-level permissions.</p>\n<p>Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network. Adversaries can often enter and explore a network with unprivileged access but require elevated permissions to follow through on their objectives. Common approaches are to take advantage of system weaknesses, misconfigurations, and vulnerabilities. Examples of elevated access include:</p>\n<ul>\n<li>SYSTEM/root level</li>\n<li>local administrator</li>\n<li>user account with admin-like access</li>\n<li>user accounts with access to specific system or perform specific function</li>\n</ul>\n<p>These techniques often overlap with Persistence techniques, as OS features that let an adversary persist can execute in an elevated context.</p>\n",
    "mandatory": false,
    "hidden": false,
    "creationDate": "2022-09-19T19:34:52.448954",
    "modificationDate": "2022-09-19T19:34:52.448954",
    "autoExtract": true,
    "tagNormalization": ""
  },
  ...
]
```


## Get a facet

To retreive a specific facet, you need its identifier.

```
curl -X 'GET' \
  'http://localhost:5001/API/Facet/666d3ecd-35b3-47ac-823a-dd8a95ecb81d' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

It then returns all the details about the facet and the enclosed tags.

```
{
  "facetId": "3f065ff7-e347-4b05-9f32-68f913a1e1d2",
  "title": "Target Geography",
  "prefix": "targetGeography",
  "description": "",
  "mandatory": false,
  "hidden": false,
  "creationDate": "2022-09-19T19:36:47.286993",
  "modificationDate": "2022-09-20T19:14:57.992239",
  "createdBy": {
    "userId": "be9e613e-697a-460b-bd4d-d79a409a1d9a",
    "userName": "automation",
    "lastActivity": "0001-01-01T00:00:00",
    "registrationDate": "2022-09-19T19:01:02.824604",
    "enabled": true,
    "friendlyName": "automation"
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
  },
  "autoExtract": true,
  "tagNormalization": "",
  "tags": [
    {
      "tagId": "2b027e6b-8f1e-4ca1-a9b6-30d8695417f4",
      "label": "colombia",
      "description": "",
      "keywords": [],
      "extractionKeywords": [],
      "backgroundColor": "bg-success-50",
      "lastModifiedBy": {
        "userId": "be9e613e-697a-460b-bd4d-d79a409a1d9a",
        "userName": "automation",
        "lastActivity": "0001-01-01T00:00:00",
        "registrationDate": "2022-09-19T19:01:02.824604",
        "enabled": true,
        "friendlyName": "automation"
      },
      "creationDate": "2022-09-19T22:36:48.052236",
      "modificationDate": "2022-09-26T13:00:27.188752",
      "friendlyName": "targetGeography:colombia"
    },
    {
      "tagId": "541a81e5-7c76-4760-a205-99801d7e51ed",
      "label": "lithuania",
      "description": "",
      "keywords": [],
      "extractionKeywords": [],
      "backgroundColor": "bg-success-50",
      "lastModifiedBy": {
        "userId": "be9e613e-697a-460b-bd4d-d79a409a1d9a",
        "userName": "automation",
        "lastActivity": "0001-01-01T00:00:00",
        "registrationDate": "2022-09-19T19:01:02.824604",
        "enabled": true,
        "friendlyName": "automation"
      },
      "creationDate": "2022-09-19T22:36:48.646141",
      "modificationDate": "2022-09-26T12:58:47.717638",
      "friendlyName": "targetGeography:lithuania"
    },
    ...
  ]
}
```

## Create a new facet

To create a new facet, you need to send a `POST` request with the details
about the facet you want to create.

```
{
  "title": "My facet",
  "prefix": "myFacet",
  "description": "<p>This is the description of my facet</p>",
  "mandatory": false,
  "hidden": false,
  "extractionRegex": "",
  "autoExtract": true,
  "tagNormalization": "upcase"
}
```

The valid values for `tagNormalization` are: ``, `camelize`, `capitalize`,
`downcase`, `handleize`, `upcase`.

That facet can be created with

```
curl -X 'POST' \
  'http://localhost:5001/API/Facet' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "title": "My facet",
  "prefix": "myFacet",
  "description": "<p>This is the description of my facet</p>",
  "mandatory": false,
  "hidden": false,
  "extractionRegex": "",
  "autoExtract": true,
  "tagNormalization": "upcase"
}'
```

The command above will return the facet as recorded by DocIntel. 

```
{
  "facetId": "133e6d06-7a66-4f79-b43b-428b2bbed29b",
  "title": "My facet",
  "prefix": "myFacet",
  "description": "<p>This is the description of my facet</p>",
  "mandatory": false,
  "hidden": false,
  "creationDate": "2022-10-27T18:52:04.117928Z",
  "modificationDate": "2022-10-27T18:52:04.117928Z",
  "createdBy": {
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
  },
  "extractionRegex": "",
  "autoExtract": true,
  "tagNormalization": "upcase"
}
```

## Edit a facet

If we wish to update the facet created in previous section, we need to send a
`PATCH` request with the `facetId` provided above. The format for providing
the body is the same as above.

That can be submited to update the comment. Note that
`723cc24c-739e-4b9a-a36e-a476aec206db` is the identifier provided in the
response property `commentId` in the section above.

```
curl -X 'PATCH' \
  'http://localhost:5001/API/Facet/133e6d06-7a66-4f79-b43b-428b2bbed29b' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "title": "My facet (updated)",
  "prefix": "myFacet",
  "description": "<p>This is the updated description of my facet</p>",
  "mandatory": false,
  "hidden": false,
  "extractionRegex": "",
  "autoExtract": true,
  "tagNormalization": "upcase"
}'
```

Again, we receive the facet as recorded.

## Delete a facet

To delete a facet, we simply send a `DELETE` request with the same identifier
we used to update the comment.

```
curl -X 'DELETE' \
  'http://localhost:5001/API/Facet/133e6d06-7a66-4f79-b43b-428b2bbed29b' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

This returns an empty `200` response. 

## Merge

To merge two facets together, you need to send a `POST` request specifying both
identifiers. The primary identifier (that is the facet that is kept) appears
first. The facet that will not remain is specified second.

For example, to merge `230c76ba-d89c-4776-8f53-1f16e845fedf` with
`7d50d1b2-e182-4863-8cf5-75deef7a5048`, you can use

```
curl -X 'POST' \
  'http://localhost:5001/API/Facet/230c76ba-d89c-4776-8f53-1f16e845fedf/Merge/7d50d1b2-e182-4863-8cf5-75deef7a5048' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '' \
```

This returns the facet matching `230c76ba-d89c-4776-8f53-1f16e845fedf`.

## Subscribe and unsubscribe

To check if you are subscribed to a facet, you need to send a `GET` query
to the endpoint `/API/Facet/$FACET_ID/Subscription`

For example, to check for the facet `3f065ff7-e347-4b05-9f32-68f913a1e1d2`, you
can use the following

```
curl -X 'GET' \
  'http://localhost:5001/API/Facet/3f065ff7-e347-4b05-9f32-68f913a1e1d2/Subscription' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

The command above would returns the following if you are not subscribed.

```
{
  "subscribed": false,
  "notify": false
}
```

You would send the following to subscribe to the facet

```
curl -X 'PUT' \
  'http://localhost:5001/API/Facet/3f065ff7-e347-4b05-9f32-68f913a1e1d2/Subscribe' \
  -H 'accept: */*'\
  -H 'Authorization: Bearer $MY_TOKEN'
```
  
The check for subscription would then return 

```
{
  "subscribed": true,
  "notify": false
}
```

If you want to subscribe and enable the notification bell, you need to send
an additional body.

```
curl -X 'PUT' \
  'http://localhost:5001/API/Facet/3f065ff7-e347-4b05-9f32-68f913a1e1d2/Subscribe' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json-patch+json' \
  -d 'true'
```

To unsubscribe, you would send

```
curl -X 'PUT' \
  'http://localhost:5001/API/Facet/3f065ff7-e347-4b05-9f32-68f913a1e1d2/Unsubscribe' \
  -H 'accept: */*'\
  -H 'Authorization: Bearer $MY_TOKEN'
```
