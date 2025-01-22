---
layout: article.njk
title: Articles
date: 2017-01-01
pagination:
  data: collections.post
  size: 20
permalink: "articles{% if pagination.pageNumber > 0 %}/page/{{ pagination.pageNumber }}{% endif %}/index.html"
metaDescription: A sample Article page listing various posts.
subtitle: A collection of technical blog posts and random thoughts
eleventyNavigation:
  key: Articles
  order: 2
---
