---
layout: default
title: Posts
---

<h1>Posts</h1>

<ul class="post-list" style="list-style:none; padding-left:0;">
  {% for post in site.posts %}
  <li style="margin-bottom: 40px;">
    
    <h2 style="margin-bottom:5px;">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </h2>

    <p style="color:#555; margin-top:0; font-size: 0.95rem;">
      {{ post.date | date: "%Y-%m-%d" }}
    </p>

    <p style="margin-top:10px; font-size:1rem; line-height:1.5;">
      {{ post.excerpt | strip_html }}
    </p>

    <!-- Read more link -->
    <p style="margin-top:12px;">
      <a href="{{ post.url | relative_url }}" style="color:#1756a9; font-weight:500;">
        Read more →
      </a>
    </p>

    <hr style="margin:40px 0;">

  </li>
  {% endfor %}
</ul>
