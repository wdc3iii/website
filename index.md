---
layout: page
title: "Home"
nav: false
nav_order: 0
---

# Welcome!

I'm Will Compton, a PhD candidate in Control and Dynamical Systems at Caltech.  
I work on control theory, machine learning, and robotics, with a focus on agile, dynamic locomotion.  
Below, you’ll find my latest papers and blog posts.

---

## Research Papers and Blog Posts

{% assign allowed_categories = "papers,blog" | split: "," %}

{% for post in site.posts %}
  {% assign post_cats = post.categories | join: "," | append: "," | split: "," %}
  {% assign intersect = post_cats | uniq | array_contains: allowed_categories %}
  {% if intersect %}
- [{{ post.title }}]({{ post.url | relative_url }}) ({{ post.date | date: "%b %-d, %Y" }})
  {% endif %}
{% endfor %}
