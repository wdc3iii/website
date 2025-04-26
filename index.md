---
layout: page
title: "Home"
nav: false
nav_order: 0
---

<style>
/* Carousel */
.carousel {
  overflow: hidden;
  height: 300px;
  position: relative;
  margin-bottom: 40px;
}
.carousel-track {
  display: flex;
  animation: scroll 30s linear infinite;
}
.carousel-track img {
  width: 33.33vw;
  height: 300px;
  object-fit: cover;
}

/* Welcome section */
.welcome {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
  font-size: 3.0rem;   /* ← bigger */
  line-height: 1.5;    /* ← bigger line spacing */
}

#heading {
  font-size: 5rem;
  margin-top: 40px;
  margin-bottom: 20px;
}

.welcome-content h1 {
    font-size: 5rem;    /* ← bigger for post titles */
}

/* Posts */
.posts {
  display: flex;
  flex-direction: column;
  gap: 40px;
  max-width: 1000px;
  margin: 60px auto;
}

.post-card {
  display: flex;
  align-items: center;
  gap: 20px;
}

.post-card img {
  width: 200px;
  height: 130px;
  object-fit: cover;
  border-radius: 12px;
}

.post-content h1 {
  font-size: 5rem;    /* ← bigger for post titles */
}


.post-content h2 {
  margin: 0;
  font-size: 4rem;    /* ← bigger for post titles */
}

.post-content h3 {
  margin: 5px 0;
  font-size: 3.0rem;  /* ← bigger for subtitles */
  color: #555;
}

.post-content p {
  margin: 8px 0 0 0;
  font-size: 2.4rem;  /* ← bigger for post meta text */
  color: #777;
}
</style>

<!-- Carousel -->
<div class="carousel">
  <div class="carousel-track">
    {% for item in site.carousel %}
      <a href="{{ item.url | relative_url }}">
        <img src="{{ item.img | relative_url }}" alt="{{ item.title }}">
      </a>
    {% endfor %}
    {% for item in site.carousel limit:3 %}
      <a href="{{ item.url | relative_url }}">
        <img src="{{ item.img | relative_url }}" alt="{{ item.title }}">
      </a>
    {% endfor %}
  </div>
</div>

<div class="carousel-debug">
  {% for item in site.carousel %}
    <div style="margin-bottom: 20px;">
      <div><strong>Title:</strong> {{ item['title'] }}</div>
      <div><strong>URL:</strong> {{ item['url'] }}</div>
      <div><strong>Absolute URL:</strong> {{ item['url'] | absolute_url }}</div>
      <div><strong>Relative URL:</strong> {{ item['url'] | relative_url }}</div>
      <div><strong>Image Path:</strong> {{ item['img'] }}</div>
    </div>
  {% endfor %}
</div>

# <span id="heading">Welcome!</span>

<div class="welcome">
I'm Will Compton, a PhD candidate in Control and Dynamical Systems at Caltech.  
I work on control theory, machine learning, and robotics, with a focus on agile, dynamic locomotion.  
Below, you’ll find my latest papers and blog posts.
</div>

---

# <span id="heading">Research Papers and Blog Posts</span>

{% assign allowed_categories = "paper,blog" | split: "," %}

<div class="posts">
{% for post in site.posts %}
  {% if post.categories contains "paper" or post.categories contains "blog" %}
    <div class="post-card">
      {% if post.image %}
      <img src="{{ post.image | relative_url }}" alt="Post image">
      {% endif %}
      <div class="post-content">
        <a href="{{ post.url | relative_url }}">
          <h2 class="post-title">{{ post.title }}</h2>
          {% if post.subtitle %}
          <h3 class="post-subtitle">{{ post.subtitle }}</h3>
          {% endif %}
        </a>
        <p class="post-meta">
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
    </div>
    <hr>
  {% endif %}
{% endfor %}
</div>