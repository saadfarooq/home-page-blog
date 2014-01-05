---
layout: default
title: Home Page
---
<h1></h1>
<p>I feel awkward writing about myself... so explore and find out for yourself.</p>
<p>The are my rambling on research, my developments activities and life in general.</p>

<div class="links">
  {% for category in site.categories %}
  <div style="display:inline-block" class="col-md-3">
    <a class="btn btn-default" href="categories/{{ category[0] }}">{{ category[0] }}</a>
  </div>
  {% endfor %}
</div>
<!--   {% for category in site.categories %}
  <li>
    <a class="btn btn-default" href="categories/{{ category[0] }}">{{ category[0] }}</a>
  </li>
  {% endfor %} -->
