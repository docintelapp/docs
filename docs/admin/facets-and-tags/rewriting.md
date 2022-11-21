---
layout: default
title: Rewriting
parent: Facets and tags
grand_parent: Administration Guide
---

# Rewriting tags

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


{: .note-title }
> From one tag to multiple tags
>
> Note that the resulting string is then split on the comma `,` to lead to the
> resulting tags. For example, you can rewrite a tag like
> *affectedIndustry:Civil Society >> International Governance (NATO/EU)* to
> *affectedOrganization:NATO* and *affectedOrganization:EU* by rewriting to
> `affectedOrganization:NATO,affectedOrganization:EU`