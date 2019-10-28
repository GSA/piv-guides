---
layout: default
title: Digital Signatures
collection: userguides
permalink: /userguides/
---

These guides will help agency users with tasks related to digitally signing Microsoft Word documents.

{% for item in site.userguides reversed %}
  {% assign link = item.permalink | remove: '/' %}
  {% if link != item.collection %}
  <hr/>
  <h3><a href="{{site.baseurl}}/{{ item.permalink }}"  title="{{ item.title }}">{{ item.title }}</a></h3>
  <strong>Date:</strong> {{ item.pubDate }}<br />
  <strong>Description:</strong> {{ item.description }}
  {% endif %}
{% endfor %}
