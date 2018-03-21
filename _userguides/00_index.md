---
layout: default
title: PIV User Guides
collection: userguides
permalink: /userguides/
---

These announcements and hot topics concern Federal Public Key Infrastucture changes that may affect your agency's operations.

{% for item in site.userguides reversed %}
  {% assign link = item.permalink | remove: '/' %}
  {% if link != item.collection %}
  <hr/>
  <h3><a href="{{site.baseurl}}/{{ item.permalink }}"  title="{{ item.title }}">{{ item.title }}</a></h3>
  <strong>Date:</strong> {{ item.pubDate }}<br />
  <strong>Description:</strong> {{ item.description }}
  {% endif %}
{% endfor %}
