---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

以下按照主导航顺序列出网站内容，方便访客快速导航。

{% assign nav = site.data.navigation.main %}

{% for item in nav %}
  {% assign url = item.url %}
  {% assign label = url | remove_first: "/" | remove: "/" %}
  <h2>{{ item.title }}</h2>

  {% comment %}
  如果是“Blog Posts”页（假设它的 URL 是 /year-archive/）
  {% endcomment %}
  {% if label == "year-archive" %}
    {% for post in site.posts %}
      {% include archive-single.html %}
    {% endfor %}

  {% else %}
    {% comment %}
    检查它是不是一个 Collection，如果是，就渲染该集合下的所有文档
    {% endcomment %}
    {% assign rendered = false %}
    {% for collection in site.collections %}
      {% if collection.label == label and collection.output %}
        {% assign rendered = true %}
        {% for doc in collection.docs %}
          {% include archive-single.html %}
        {% endfor %}
      {% endif %}
    {% endfor %}

    {% comment %}
    如果它不是 Collection，再尝试把它当普通页面渲染
    {% endcomment %}
    {% unless rendered %}
      {% assign pages = site.pages | where: "url", url %}
      {% if pages.size > 0 %}
        {% assign p = pages[0] %}
        {% include archive-single.html page=p %}
      {% endif %}
    {% endunless %}
  {% endif %}
{% endfor %}
