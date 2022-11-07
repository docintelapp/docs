---
layout: default
title: Tags
parent: Administration Guide
---

# Facets and tags

This section documents how facets and tags can be configured to make the life of
users easier.

## Automated extraction

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

## Normalizing tags

Users (except you, of course) are not always very good at using the same
convention every time, especially among a large team. Sometimes, someone will
write *APT10* and sometimes *apt10* or *Apt10*. This does not look as good as
always using the same convention. 

To that effect, DocIntel can normalize the tags when they are created. The
supported normalizations are described in the following table.

| Normalization | Description                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Camelize      | Converts a string to CamelCase.                                                                                         |
| Capitalize    | Capitalizes the first word in a string.                                                                                 |
| Downcase      | Converts a string to all lowercase characters.                                                                          |
| Handleize     | Converts a string into a handle (lowercase where all whitespace and special characters are replaced with a hyphen `-`). |
| Upcase        | Converts a string to all uppercase characters.                                                                          |

## Rewriting tags

Previous section showed how you can normalize the tags so that users don't need
to remember the convention that was decided for the team. However, sometimes,
users can also forget that specific keywords were chosen and keep using others.

For example, *TLP:WHITE* was replaced by *TLP:CLEAR*. However, many articles,
reports and other sources still use the old convention. And some users might
forget that now, they have to use *TLP:CLEAR* instead.

Another example includes vendors that use specific prefix or tags to annotate
their documents. A vendor could use  *Retail Banks/ATMs/Credit Cards*, *Equity
Management/Investment Banking*, *Banks*, *Equity Management/Investment
Banking/Brokerage/Exchanges*, and *Financial Services >> Retail
Banks/ATMs/Credit Cards* for their reports while your are only interested by a
more global tag *Financial Sector*. You don't want all these tags in your system
when you import the feed.

DocIntel allow you to create **rewriting rules** to rewrite the tags when they
are input by a user, or imported with an importer.

{: .warning } 

This code is under review and improvement. Differences between your version and
the documentation might occurs. [Let us
know](https://github.com/docintelapp/docs/issues) if you spot any discrepancies.

To create a rewriting rules, you first need to rewrite a ruleset. A ruleset will
help you keep your rewriting rules more organized. For example, you can have a
ruleset for each vendor, for TLP, and one for your own organization.

Once you created a ruleset, you can add a rule. You need to specify a name, a
description, a pattern as a regular expression, and a replacement. You can use
groups to replace matched elements. We recommend you to use
[https://regex101.com/](https://regex101.com/) to test your rules (select the
.NET engine, and the substitution function).

![](/docs/admin/assets/imgs/regex101.png){:.screenshot}

For example, you can decide to rewrite all tags *actors:...* to *groups:...*, to
that effect, you can define a rule as follow:

* Name: Rewrite actor to group
* Pattern: `^actor:(?<name>.*)$`
* Replacement: `group:${name}`

The complete documentation for regular expressions as handled in .NET is
available
[here](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions).