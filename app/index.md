---
layout: default
title: Home Page
---
<h1></h1>
<p>I feel awkward writing about myself... so explore and find out for yourself.</p>
<p>The are my rambling on research, my developments activities and life in general.</p>

<div id="contact-list" class="text-center">
  <ul class="list-unstyled list-inline">
    {% for category in site.categories %}
    <li>
      <a class="btn btn-default btn-sm" href="categories/{{ category[0] }}">
        {{ category[0] }}
      </a>
    </li>
    {% endfor %}
  </ul>
</div>

<hr>
<h1>Recent Posts <small>In any category</small></h1>
<ul class="posts">
    {% for post in site.posts limit: 10 %}
      <li>
        <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
        <p>{{ post.date | date_to_string }}</p>
        <p>
          {{ post.content | strip_html | truncatewords:50 }}
        </p>
        <p>
          <a href="{{ post.url }}">Read more...</a>
        </p>
      </li>
    {% endfor %}
  </ul>
