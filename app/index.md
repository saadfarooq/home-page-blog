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
