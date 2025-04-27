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
  height: 300px; /* controls max visible height */
  position: relative;
  margin-bottom: 40px;
}

.carousel-track img {
  height: 100%;
  width: auto;
  object-fit: contain;
  flex-shrink: 0;
  transition: transform 0.5s ease; /* smooth zoom */
}

.carousel-track img:hover {
  transform: scale(1.1); /* zoom 10% */
  z-index: 2;            /* bring hovered image above neighbors */
}

.carousel-track img {
  height: 100%;           /* fill vertically */
  width: auto;            /* let width adjust automatically */
  object-fit: contain;    /* show whole image, no cutting */
  flex-shrink: 0;         /* don't squish */
  padding: 0 10px;        /* optional: slight side padding between images */
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

.post-card img {
  width: 100%;
  height: auto;
  margin: 20px 0;
  border-radius: 8px;
  transition: transform 0.3s ease;
}

.post-card img:hover {
  transform: scale(1.05);
}
</style>

<!-- Carousel -->
<div class="carousel">
  <div class="carousel-track">
    {% for item in site.carousel %}
      <a href="{{ item.link_url | relative_url }}">
        <img src="{{ item.img }}" alt="{{ item.title }}">
      </a>
    {% endfor %}
    {% for item in site.carousel %}
      <a href="{{ item.link_url | relative_url }}">
        <img src="{{ item.img }}" alt="{{ item.title }}">
      </a>
    {% endfor %}
  </div>
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
      <div class="post-content">
        <a href="{{ post.url | relative_url }}">
          <h2 class="post-title">{{ post.title }}</h2>
        </a>

        {% if post.thumbnail-img %}
        <a href="{{ post.url | relative_url }}">
          <img src="{{ post.thumbnail-img }}" alt="{{ post.title }}">
        </a>
        {% endif %}

        {% if post.subtitle %}
        <h3 class="post-subtitle">{{ post.subtitle }}</h3>
        {% endif %}

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

<script>
document.addEventListener('DOMContentLoaded', function() {
  const track = document.querySelector('.carousel-track');
  const images = document.querySelectorAll('.carousel-track img');

  let index = 0;
  let currentOffset = 0;
  let paused = false;   // <-- NEW

  // When hover, pause
  images.forEach(img => {
    img.addEventListener('mouseenter', () => paused = true);
    img.addEventListener('mouseleave', () => paused = false);
    });

  setInterval(() => {
    if (paused) return;  // <-- NEW

    const nextImage = images[index];
    const nextImageWidth = nextImage.offsetWidth;

    currentOffset += nextImageWidth;
    track.style.transform = `translateX(${-currentOffset}px)`;

    index++;

    if (index >= images.length / 2) {
      setTimeout(() => {
        track.style.transition = 'none';
        track.style.transform = 'translateX(0)';
        currentOffset = 0;
        index = 0;
        setTimeout(() => {
          track.style.transition = 'transform 1s ease';
        }, 50);
      }, 1000);
    }
  }, 15000);
});
</script>