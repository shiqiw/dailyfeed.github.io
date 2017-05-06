---
layout: post
title: "Recommendation"
date: 2017-05-06
permalink: /win/:year/:month/:day/:title
section: "win"
---

This post is reserved for the recommentation system related knowledge. It will be enriched on a daily basis. The goal is to come up with idea to build a vacation destination recommentation system.

## Case study

Youtube, recommending videos to watch
- Machine learning is the common approach, but heuristic solutions (e.g. based on author, popularity) works for very few data, or fast minimal solution scenarios.
- User-based or item-based collaborative filtering is a popular technique for recommendation system. 
- Pick the right explicit and implicit feature to use. For example, like/share/subscribe (explicit), watch time (implicit), video title/labels/categories (explicit), freshness (explicit). Picking the right set of feature needs experiments.
- Infrastructure should be split into online and offline parts (Netflix has 3 parts). Offine part for data storage, model training and update, online part for recommendation, filtering and ranking on the fly.

## References
1. [Design a Recommendation System](http://blog.gainlo.co/index.php/2016/05/24/design-a-recommendation-system/)