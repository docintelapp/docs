---
layout: default
title: Automated extraction
parent: Facets and tags
grand_parent: Administration Guide
---

# Automated tag extraction

Tags can be automatically extracted from document (in fact, files) when they are
processed before their registration.

There are two ways for extracting tags:

* Using keywords in tags,
* Using a regular expression, that will create new tags in a facet.

### Automated extraction with keywords

By default, when the checkbox "Auto extract" is enabled, DocIntel will look for
the exact label of the tag (regardless the casing).

For example, 

* If you have a tag *Russia* in a facet *sourceGeography* with automated
  extraction enabled, any document that you upload that contains the word *Russia*
  will be automatically annotated with that tag.

* If you have a tag *NOBELIUM* in a facet *actor.microsoft* with automated
  extraction, any document that mentions the word *NOBELIUM* (or *Nobelium*) will be tagged
  accordingly.

However, if you have a tag titled *T1003.003 - OS Credential Dumping: NTDS* and
you upload a file with the word *T1003.003*, the document will be not be tagged
automatically as there is no exact match. To fill that gap, you can specify, in
the tag edit page, extraction keywords. For that tag, you could add keywords
like *T1003.003* or *NTDS* but also related keywords like *secretsdump.py*,
*ntdsutil.exe* or *Invoke-NinjaCopy* as mentionned in the page [OS Credential
Dumping: NTDS](https://attack.mitre.org/techniques/T1003/003/) from MITRE. This
is a great way to make tagging faster.

{: .note } 

Avoid very generic terms that would match all your documents. Tagging should not
replace search but should help you have a structured information about the
document.

### Automated extraction with a regular expression

The previous section documented how keywords can be used to make tagging more
efficient. However, it requires you to know and encode all the possible tags
even if they follow a specific pattern.

For example, Mandiant names its actors according to a convention. As they
explain in [this
article](https://vision.fireeye.com/editions/10/10-mandiant-graduation.html),
their naming conventions title groups with APT, UNC or FIN followed by a number.
In the same article Mandiant mention they are tracking more than 2000 groups.
You certainly do not want to spend hours creating these tags manually, nor do
you want these tags without any document attached.

To fill that need, you can specify a regular expression for a facet. If the
expression matches, DocIntel will create a new tag with the match as a label.

The following table provides example of regular expression that could be useful for a CTI team:

| Regular Expression                                      | Description                   | Suggested facet   |
| ------------------------------------------------------- | ----------------------------- | ----------------- |
| `CVE-\d{4}-\d{4,7}`                                     | Matches CVE numbers           | *vulnerability*   |
| `(APT|FIN|UNC)\d{1,4}`                                  | Matches Mandiant group names  | *actor.mandiant*  |
| `APT-C-\d{1,4}`                                         | Matches 360.net group names   | *actor.360*       |
| `DEV-\d{1,4}`                                           | Matches Microsoft group names | *actor.microsoft* |
| `TLP[\s:_\-](red|amber|white|clear|green|amber+strict)` | Matches common TLP notations  | *tlp*             |

{: .note } 

If you have other ideas for regular expression, please reach out so we can
update the table above for the whole cyber threat intelligence community.
