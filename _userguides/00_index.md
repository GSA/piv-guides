---
layout: default
title: PIV User Guides
collection: userguides
permalink: /userguides/
---

These user guides will help agency users with PIV related tasks.

{% for item in site.userguides reversed %}
  {% assign link = item.permalink | remove: '/' %}
  {% if link != item.collection %}
  <hr/>
  <h3><a href="{{site.baseurl}}/{{ item.permalink }}"  title="{{ item.title }}">{{ item.title }}</a></h3>
  <strong>Date:</strong> {{ item.pubDate }}<br />
  <strong>Description:</strong> {{ item.description }}
  {% endif %}
{% endfor %}
