---
layout: default
title: Normalizing tags
parent: Facets and tags
grand_parent: Administration Guide
---

# Normalizing tags

Users are not always very good at using the same convention every time,
especially among a large team. Sometimes, someone will write *APT10* and
sometimes *apt10* or *Apt10*. This does not look as good as always using the
same convention.

To that effect, DocIntel can normalize the tags when they are created. The
supported normalizations are described in the following table.

| Normalization | Description                                                                                                             |
| ------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Camelize      | Converts a string to CamelCase.                                                                                         |
| Capitalize    | Capitalizes the first word in a string.                                                                                 |
| Downcase      | Converts a string to all lowercase characters.                                                                          |
| Handleize     | Converts a string into a handle (lowercase where all whitespace and special characters are replaced with a hyphen `-`). |
| Upcase        | Converts a string to all uppercase characters.                                                                          |

