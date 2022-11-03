---
layout: default
title: Importers
parent: Administration Guide
---

# Importers

Importers are the cornerstone of DocIntel's automated scraping capability. It's
how you can keep your hands off the keyboard, and let DocIntel do all the work
for you.

Importers allow you to automate the submission of URLs to the
[scrapers](/docs/admin/scrapers/). Importers are configurable to your specific
needs, so you can tailor them to your workflow and make them work with whatever
systems you already have in place.

For example, they allow you to automatically import data from RSS feeds and
send the URLs to scrape to the Readability scraper. 

## How to collect RSS feeds?

To collect information from RSS feeds, you first need to [configure a
scraper](/docs/admin/scrapers/#how-to-collect-web-pages) that will scrape the
webpages for you. Then, follow the steps:

1. Go to Administration, then Importers in the left menu
2. Click on Install
3. Select RSS Source Importer for the *Importer* field
3. Enable it, define a collection delay (that is how often the importer checks
   the feeds). You can also customize the rest, but so far, we don't recommend
   additional customization for this importer.
4. Click Save

DocIntel is now configured to automatically check RSS feeds. But we have not
configured any feed at the moment, so nothing will be imported.

To import a feed, you need to attach it to a source. So, create a new source
(Sources, then Add Source on the left menu) or go to an existing one. Then,

Click on Edit, then at the bottom, you have a panel titled "Syndication". In
the panel you can configure the URL to the RSS feed and indicates that you 
want DocIntel to scrape it automatically. 

![](/docs/admin/assets/imgs/configure-syndication.png){:.screenshot}

The field RSS keywords can be used to only scrape RSS items that contains one
of the space separated word. 

Save the source, and now, DocIntel will automatically check the RSS feed. It
will submit the URLs to the scrapers, than will collect the information for
you, submit it to the analyzer for the pre-processing step and then you to
register.
