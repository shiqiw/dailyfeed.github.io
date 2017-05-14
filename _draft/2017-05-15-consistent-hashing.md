---
layout: post
title: "Consistent hashing"
date: 2017-05-15
permalink: /knowledge/:year/:month/:day/:title
section: "knowledge"
---

Last time, we mentioned that *consistent hashing could be considered a composite of hash and list partitioning where the hash reduces the key space to a size that can be listed*. Today, we are going to unveil consistent hashing.

If queries regularly retrieve data by using a combination of attribute values, it may be possible to define a composite shard key by concatenating attributes together. Alternatively, use a pattern such as Index Table to provide fast lookup to data based on attributes that are not covered by the shard key.
