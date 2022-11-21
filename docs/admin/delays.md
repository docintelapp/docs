---
layout: default
title: Delay
parent: Administration Guide
---

# Delays


All of the following questions might have been running through your mind: "Why
doesn't my document show up in search?", "Why is a deleted tag still being
displayed in my search results?", or even, "why is the document count in source
search not correct?" The answer to all of these questions is that DocIntel
works asynchronously and some delays take place for performance tradeoffs.

## Indexing Delay

A message is sent to a background worker after you have edited a document,
notifying that the index needs an update. We don't do this synchronously so
that the user does not have to wait. The background worker then starts and
indexes the document in Apache Solr. The documents usually appear in search
results eventually, but might not show up immediately because Apache Solr
doesn't update its index nor write every change to disk for performance's sake;
it's faster to write 10 documents at once than write 10 times separately.

Apache Solr uses two measures to decide if it has to commit the index: the
number of pending changes and the delay. You can change both values in the
configuration for each index, depending on your environment's needs. Depending
on how Apache Solr is installed, look for
`DATA/solr/data/document/conf/solrconfig.xml` for documents. In that file,
there will be a fragment that controls how fast data is written to disk;
maxTime is specified in milliseconds.

```xml
<autoCommit>
   <maxDocs>100</maxDocs>
   <maxTime>15000</maxTime>
   <openSearcher>false</openSearcher>
  </autoCommit>
```

This fragment dictates how quickly the update will be reflected in the index;
maxTime is calculated in milliseconds.

```xml
  <autoSoftCommit>
   <maxTime>1000</maxTime>
  </autoSoftCommit>
```

The following timeline shows the delays.

{:.text-center}

![](/docs/admin/assets/imgs/timing.png)

## Indexer delay

As well as the aforementioned setback, we face two additional obstacles. The
first is that the indexer could be halted or might miss a message. The second
obstacle is that some updates don't need to take place in near-real time; an
example of this would be documents count in sources and tags. This conserves
performance .

If we didn't have an additional mechanism, the document, tag, or source
wouldn't be indexed unless edited again. The indexers do extra checks of the
database and index regularly to make sure that everything is in sync. These
delays can be configured in the DocIntel configuration file `appSettings.json`
within a section Schedule. They might need tuning according to your environment
and requirements. All delays are expressed in minutes.

```json
"Schedule": {
  "MaxIndexingDelay": 30,
  "AnalyzerFrequencyCheck": 30,
  "IndexingFrequencyCheck": 30
}
```

The following timeline shows the delays.

{:.text-center}

![](/docs/admin/assets/imgs/frequent-checks.png)