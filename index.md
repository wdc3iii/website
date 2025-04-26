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

{% assign allowed_categories = "paper,blog" | split: "," %}

{% for post in site.posts %}
    {% if post.categories contains "paper" or post.categories contains "blog" %}

<div class="post-preview">
    <a href="{{ post.url | relative_url }}">
        <h2 class="post-title">{{ post.title }}</h2>
        {% if post.subtitle %}
        <h3 class="post-subtitle">{{ post.subtitle }}</h3>
        {% endif %}
    </a>
    <p class="post-meta" style="margin-bottom:5px">
        Posted by {{ post.author }} on {{ post.date | date: "%B %-d, %Y" }}
    </p>
    <div class="notepad-index-post-tags">
        {% for tag in post.tags %}
            <a href="{{ '/search/index.html#' | append: tag | cgi_encode | relative_url }}" title="Other posts from the {{ tag | capitalize }} tag">
                {{ tag | capitalize }}
            </a>{% unless forloop.last %}&nbsp;{% endunless %}
        {% endfor %}
    </div>
</div>

<hr>

    {% endif %}
{% endfor %}
