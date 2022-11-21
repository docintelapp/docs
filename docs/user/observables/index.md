---
layout: default
title: Observables
parent: User Guide
---

# Observables

In DocIntel, observables are technical elements such as IP addresses, or domain
names that allow analyst to detect, respond, or understand cyber threats.
DocIntel stores all the obserables in a Vertex Synapse database. The database
comes with a very powerful and mature data model, as seen in [Synapse
documentation](https://synapse.docs.vertex.link/en/latest/synapse/).

The tags associated with observables are not DocIntel tags but Synapse tags. We
decided to keep both separate as their annotate different objects at different
abstraction level, with a different granularity.

## How observables are extracted?

Observables are extracted based on regular expressions. The results of the
matches are then automatically reviewed to exclude the most likely false
positive. In doubt, DocIntel will add a tag `_di.Review` to the tag to indicate
the user that this extracted observable is likely to yield false positive. The
observables are extracted by the document analyzer.

When extracted, the observables are not added to the database of observables
until they are reviewed. They are added to a specific layer of the database
(called a [Synapse view](https://synapse.docs.vertex.link/en/latest/synapse/glossary.html#view))
that is a [fork](https://synapse.docs.vertex.link/en/latest/synapse/glossary.html#fork)
of the main database layer. 