---
layout: default
title: Security
parent: Administration Guide
---

# Security Settings

## DTD processing 

At the beginning of some of your ingested feeds, you might find a DOCTYPE
sequence among other characters. This declaration permits an XML processor to
validate the document against pre-specified declarations which state what
values or contents a set of elements and attributes can have. Because data
expansion is easy to do with entity processing, some security-focused
individuals believe that DTD validation—or running entities without validating
them—presents a risk. By doing this, it's possible to take very small XML data
and turn it into a much larger document. That's why DocIntel is warning you
that your information might not be secure.

You have the option to define the policy for doctype declaration processing in
your `appsettings.json` file. The available options are Prohibit (0), Ignore
(1), or Parse (2). This will enable you to ignore the DOCTYPE and allow for the
successful ingestion of these feeds. For example, you can include (between the
main curly braces) the following into your configuration file
`appsettings.json`.

```
"Security": {
  "DtdProcessing": 1
}
```

## Sensitive Data Logging

For debugging purposes, you may want to see the values in your messages and
logging. This setting `EnableSensitiveDataLogging` enables application data to
be included in exception messages, logging, etc. This can include usernames and
passwords. You should only enable this flag if you have the appropriate
security measures in place based on the sensitivity of this data. We do not
recommend enabling this security setting in your production environment unless
you are sure of what you are doing.

```
"Security": {
  "EnableSensitiveDataLogging": true
}
```