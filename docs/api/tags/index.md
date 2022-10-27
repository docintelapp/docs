---
layout: default
title: Tags
parent: API
---

# API for Tags

This page describes how to retreive all tags, create, update, merge and delete
tags but as well how users can subscribe to tags.

| Action | Endpoint | Description |
| ------ | -------- | ----------- |
| `GET` | `/API/Tag` | Get all tags |
| `POST` | `/API/Tag` | Create a new tag |
| `GET` | `/API/Tag/{tagId}` | Get tag `tagId` |
| `PATCH` | `/API/Tag/{tagId}` | Update tag `tagId` |
| `DELETE` | `/API/Tag/{tagId}` | Delete tag `tagId` |
| `GET` | `/API/Tag/{tagId}/Subscription` | Get subscription for `tagId` |
| `POST` | `/API/Tag/{tagId}/Subscribe` | Subscribe to `tagId` |
| `POST` | `/API/Tag/{tagId}/Unsubscribe` | Unsubscribe from `tagId` |
| `POST` | `/API/Tag/{primaryId}/Merge/{secondaryId}` | Merge tags `primaryId` with `secondaryId` |

{: .note }
> We assume that the user is authenticated, either with a JWT token or with 
> a Cookie, for example when using the Swagger interface. For the examples, 
> we assume that the application is running on `http://localhost:5001`.

## Get all tags

To retreive all tags known by DocIntel, 

```
curl -X 'GET' \
  'http://localhost:5001/API/Tag' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

It then returns all tags (output is truncated for the documentation
convenience).

```
[
  {
    "tagId": "0182cbee-5c90-4e87-b91a-de7577928066",
    "label": "T1620 - Reflective Code Loading",
    "description": "<p>Adversaries may reflectively load code into a process in order to conceal the execution of malicious payloads. Reflective loading involves allocating then executing payloads directly within the memory of the process, vice creating a thread or process backed by a file path on disk. Reflectively loaded payloads may be compiled binaries, anonymous files (only present in RAM), or just snubs of fileless executable code (ex: position-independent shellcode).(Citation: Introducing Donut)(Citation: S1 Custom Shellcode Tool)(Citation: Stuart ELF Memory)(Citation: 00sec Droppers)(Citation: Mandiant BYOL)</p>\n<p>Reflective code injection is very similar to <a href=\"https://attack.mitre.org/techniques/T1055\">Process Injection</a> except that the “injection” loads code into the processes’ own memory instead of that of a separate process. Reflective loading may evade process-based detections since the execution of the arbitrary code may be masked within a legitimate or otherwise benign process. Reflectively loading payloads directly into memory may also avoid creating files or other artifacts on disk, while also enabling malware to keep these payloads encrypted (or otherwise obfuscated) until execution.(Citation: Stuart ELF Memory)(Citation: 00sec Droppers)(Citation: Intezer ACBackdoor)(Citation: S1 Old Rat New Tricks)</p>\n",
    "keywords": [
      "T1620"
    ],
    "extractionKeywords": [
      "T1620"
    ],
    "backgroundColor": "bg-success-50",
    "creationDate": "2022-09-19T22:34:52.92572",
    "modificationDate": "2022-09-24T14:52:12.222097",
    "facet": {
      "facetId": "666d3ecd-35b3-47ac-823a-dd8a95ecb81d",
      "title": "Technique (Defense Evasion)",
      "prefix": "technique.defenseEvasion",
      "description": "<p>The adversary is trying to avoid being detected.</p>\n<p>Defense Evasion consists of techniques that adversaries use to avoid detection throughout their compromise. Techniques used for defense evasion include uninstalling/disabling security software or obfuscating/encrypting data and scripts. Adversaries also leverage and abuse trusted processes to hide and masquerade their malware. Other tactics’ techniques are cross-listed here when those techniques include the added benefit of subverting defenses.</p>\n",
      "mandatory": false,
      "hidden": false,
      "creationDate": "2022-09-19T19:34:52.460488",
      "modificationDate": "2022-09-19T19:34:52.460488",
      "autoExtract": true,
      "tagNormalization": "",
      "tags": []
    },
    "friendlyName": "technique.defenseEvasion:T1620 - Reflective Code Loading"
  },
  {
    "tagId": "009f6d2f-45be-47af-a3cc-dbe17ba252fd",
    "label": "T1547.003 - Time Providers",
    "description": "<p>Adversaries may abuse time providers to execute DLLs when the system boots. The Windows Time service (W32Time) enables time synchronization across and within domains.(Citation: Microsoft W32Time Feb 2018) W32Time time providers are responsible for retrieving time stamps from hardware/network resources and outputting these values to other network clients.(Citation: Microsoft TimeProvider)</p>\n<p>Time providers are implemented as dynamic-link libraries (DLLs) that are registered in the subkeys of  <code>HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Services\\W32Time\\TimeProviders&lt;/code&gt;.(Citation: Microsoft TimeProvider) The time provider manager, directed by the service control manager, loads and starts time providers listed and enabled under this key at system startup and/or whenever parameters are changed.(Citation: Microsoft TimeProvider)</p>\n<p>Adversaries may abuse this architecture to establish persistence, specifically by registering and enabling a malicious DLL as a time provider. Administrator privileges are required for time provider registration, though execution will run in context of the Local Service account.(Citation: Github W32Time Oct 2017)</p>\n",
    "keywords": [
      "T1547.003"
    ],
    "extractionKeywords": [
      "T1547.003"
    ],
    "backgroundColor": "bg-success-50",
    "creationDate": "2022-09-19T22:34:53.525987",
    "modificationDate": "2022-09-19T22:34:53.525993",
    "facet": {
      "facetId": "72af578f-7274-4d39-8910-4f4d2137dfe6",
      "title": "Technique (Privilege Escalation)",
      "prefix": "technique.privilegeEscalation",
      "description": "<p>The adversary is trying to gain higher-level permissions.</p>\n<p>Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network. Adversaries can often enter and explore a network with unprivileged access but require elevated permissions to follow through on their objectives. Common approaches are to take advantage of system weaknesses, misconfigurations, and vulnerabilities. Examples of elevated access include:</p>\n<ul>\n<li>SYSTEM/root level</li>\n<li>local administrator</li>\n<li>user account with admin-like access</li>\n<li>user accounts with access to specific system or perform specific function</li>\n</ul>\n<p>These techniques often overlap with Persistence techniques, as OS features that let an adversary persist can execute in an elevated context.</p>\n",
      "mandatory": false,
      "hidden": false,
      "creationDate": "2022-09-19T19:34:52.448954",
      "modificationDate": "2022-09-19T19:34:52.448954",
      "autoExtract": true,
      "tagNormalization": "",
      "tags": []
    },
    "friendlyName": "technique.privilegeEscalation:T1547.003 - Time Providers"
  },
  ...
]
```

Note that the list is paginated, so you will only get the 10 first tags. To
get the second page, you need to specify it. The pagination starts at `1`, 
requesting the page `0` returns all tags.

```
curl -X 'GET' \
  'http://localhost:5001/API/Tag?page=2' \
  -H 'accept: application/json'
```

## Get a tag

To retreive a specific tag, you need its identifier. For example,
`009f6d2f-45be-47af-a3cc-dbe17ba252fd` as seen in the list above.

```
curl -X 'GET' \
  'http://localhost:5001/API/Tag/009f6d2f-45be-47af-a3cc-dbe17ba252fd' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

It then returns all the details about the facet and the enclosed tags.

```
{
  "tagId": "009f6d2f-45be-47af-a3cc-dbe17ba252fd",
  "label": "T1547.003 - Time Providers",
  "description": "<p>Adversaries may abuse time providers to execute DLLs when the system boots. The Windows Time service (W32Time) enables time synchronization across and within domains.(Citation: Microsoft W32Time Feb 2018) W32Time time providers are responsible for retrieving time stamps from hardware/network resources and outputting these values to other network clients.(Citation: Microsoft TimeProvider)</p>\n<p>Time providers are implemented as dynamic-link libraries (DLLs) that are registered in the subkeys of  <code>HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Services\\W32Time\\TimeProviders&lt;/code&gt;.(Citation: Microsoft TimeProvider) The time provider manager, directed by the service control manager, loads and starts time providers listed and enabled under this key at system startup and/or whenever parameters are changed.(Citation: Microsoft TimeProvider)</p>\n<p>Adversaries may abuse this architecture to establish persistence, specifically by registering and enabling a malicious DLL as a time provider. Administrator privileges are required for time provider registration, though execution will run in context of the Local Service account.(Citation: Github W32Time Oct 2017)</p>\n",
  "keywords": [
    "T1547.003"
  ],
  "extractionKeywords": [
    "T1547.003"
  ],
  "backgroundColor": "bg-success-50",
  "creationDate": "2022-09-19T22:34:53.525987",
  "modificationDate": "2022-09-19T22:34:53.525993",
  "facet": {
    "facetId": "72af578f-7274-4d39-8910-4f4d2137dfe6",
    "title": "Technique (Privilege Escalation)",
    "prefix": "technique.privilegeEscalation",
    "description": "<p>The adversary is trying to gain higher-level permissions.</p>\n<p>Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network. Adversaries can often enter and explore a network with unprivileged access but require elevated permissions to follow through on their objectives. Common approaches are to take advantage of system weaknesses, misconfigurations, and vulnerabilities. Examples of elevated access include:</p>\n<ul>\n<li>SYSTEM/root level</li>\n<li>local administrator</li>\n<li>user account with admin-like access</li>\n<li>user accounts with access to specific system or perform specific function</li>\n</ul>\n<p>These techniques often overlap with Persistence techniques, as OS features that let an adversary persist can execute in an elevated context.</p>\n",
    "mandatory": false,
    "hidden": false,
    "creationDate": "2022-09-19T19:34:52.448954",
    "modificationDate": "2022-09-19T19:34:52.448954",
    "autoExtract": true,
    "tagNormalization": "",
    "tags": []
  },
  "friendlyName": "technique.privilegeEscalation:T1547.003 - Time Providers"
}
```

## Create a new tag

To create a new tag, you need to send a `POST` request with the details
about the tag you want to create. For example, assuming a facet
`6c731483-76db-40af-87f0-fb09edb3cf0a` for the tools, we can describe the
tag `Sliver` by the following JSON:

```
{
  "label": "Sliver",
  "description": "Sliver is designed to be an open source alternative to Cobalt Strike.",
  "keywords": [],
  "extractionKeywords": [],
  "backgroundColor": "bg-primary-300",
  "facetId": "6c731483-76db-40af-87f0-fb09edb3cf0a"
}
```

We can then send the JSON above to the API to create the tag.

```
curl -X 'POST' \
  'http://localhost:5001/API/Tag' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "label": "Sliver",
  "description": "Sliver is designed to be an open source alternative to Cobalt Strike.",
  "keywords": [],
  "extractionKeywords": [],
  "backgroundColor": "bg-primary-300",
  "facetId": "6c731483-76db-40af-87f0-fb09edb3cf0a"
}'
```

The command above will return the newly recorded tag:

```
{
  "tagId": "9443df7b-d1da-4ca8-be8f-3395a92d31ac",
  "label": "Sliver",
  "description": "Sliver is designed to be an open source alternative to Cobalt Strike.",
  "keywords": [],
  "extractionKeywords": [],
  "backgroundColor": "bg-primary-300",
  "creationDate": "2022-10-27T22:30:06.900758+02:00",
  "modificationDate": "2022-10-27T22:30:06.900764+02:00",
  "facet": {
    "facetId": "6c731483-76db-40af-87f0-fb09edb3cf0a",
    "title": "Tool",
    "prefix": "tool",
    "description": "",
    "mandatory": false,
    "hidden": false,
    "creationDate": "2022-09-20T19:36:12.732588",
    "modificationDate": "2022-09-21T05:19:49.579922",
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
    "autoExtract": true,
    "tagNormalization": "",
    "tags": []
  },
  "friendlyName": "tool:Sliver"
}
```

As we can see in the user interface, the tag was properly created.

![](/docs/api/assets/imgs/facet-new-tag.png){:.screenshot}

## Edit a tag

If we wish to update the tag created in previous section, we need to send a
`PATCH` request with the `tagId` provided above. The format for providing
the body is the same as above. For example,

```
{
  "label": "Sliver",
  "description": "Sliver is designed to be an open source alternative to Cobalt Strike.",
  "keywords": [],
  "extractionKeywords": [],
  "backgroundColor": "bg-primary-500",
  "facetId": "6c731483-76db-40af-87f0-fb09edb3cf0a"
}
```

That can be submited to update the comment. Note that
`9443df7b-d1da-4ca8-be8f-3395a92d31ac` is the identifier provided in the
response property `tagId` in the section above.

```
curl -X 'PATCH' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json-patch+json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '{
  "label": "Sliver",
  "description": "Sliver is designed to be an open source alternative to Cobalt Strike.",
  "keywords": [],
  "extractionKeywords": [],
  "backgroundColor": "bg-primary-500",
  "facetId": "6c731483-76db-40af-87f0-fb09edb3cf0a"
}'
```

The API call returns the updated tag.

## Delete a tag

To delete a tag, we simply send a `DELETE` request with the same identifier
we used to update the comment.

```
curl -X 'DELETE' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer $MY_TOKEN'
```

This returns an empty `200` response. 

## Merge

To merge two tags together, you need to send a `POST` request specifying both
identifiers. The primary identifier (that is the tags that is kept) appears
first. The tags that will not remain is specified second.

For example, assume that we created a second tag `Silver` (notice the typo) 
that has identifier `18c7becb-800b-4d54-9c9c-0f1e7b06d9b0`. We want to merge
it with the correct tag `Sliver` (that has identifier 
`9443df7b-d1da-4ca8-be8f-3395a92d31ac`). We can use

```
curl -X 'POST' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac/Merge/18c7becb-800b-4d54-9c9c-0f1e7b06d9b0' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -d '' \
```

This returns the tags matching `9443df7b-d1da-4ca8-be8f-3395a92d31ac`.

## Subscribe and unsubscribe

To check if you are subscribed to a tag, you need to send a `GET` query
to the endpoint `/API/Tag/$TAG_ID/Subscription`

For example, to check for the tags `9443df7b-d1da-4ca8-be8f-3395a92d31ac`, you
can use the following

```
curl -X 'GET' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac/Subscription' \
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

You would send the following to subscribe to the tags

```
curl -X 'PUT' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac/Subscribe' \
  -H 'accept: */*' \
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
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac/Subscribe' \
  -H 'accept: */*'  \
  -H 'Authorization: Bearer $MY_TOKEN' \
  -H 'Content-Type: application/json-patch+json' \
  -d 'true'
```

To unsubscribe, you would send

```
curl -X 'PUT' \
  'http://localhost:5001/API/Tag/9443df7b-d1da-4ca8-be8f-3395a92d31ac/Unsubscribe' \
  -H 'accept: */*'\
  -H 'Authorization: Bearer $MY_TOKEN'
```
