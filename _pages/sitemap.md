---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

以下列出本站的所有页面和条目，方便访客快速导航。

{% comment %}
1. 先取出所有主导航的 URL 列表
{% endcomment %}
{% assign nav_urls = site.data.navigation.main | map: "url" %}


<h2>Pages</h2>
{% comment %}
2. 遍历所有页面，只渲染那些 URL 在主导航里的页面
{% endcomment %}
{% for page in site.pages %}
  {% if nav_urls contains page.url %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}


<h2>Posts</h2>
{% for post in site.posts %}
  {% include archive-single.html %}
{% endfor %}


{% comment %}
3. 遍历所有 collection（除了 posts），
   只有当其 archive URL 在主导航里才会渲染
{% endcomment %}
{% for collection in site.collections %}
  {% if collection.label != "posts" %}
    {% capture archive_url %}\/{{ collection.label }}\/{% endcapture %}
    {% if nav_urls contains archive_url %}
      <h2>{{ collection.label | capitalize }}</h2>
      {% for doc in collection.docs %}
        {% include archive-single.html %}
      {% endfor %}
    {% endif %}
  {% endif %}
{% endfor %}
