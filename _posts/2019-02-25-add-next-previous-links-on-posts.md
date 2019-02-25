---
layout: post
title: Add next/previous links on posts
date: 2019-02-25 01:06 +0000
category: metablogging
tags: jekyll
---

This one was much simpler than creating the tag pages. Jekyll has 
`page.previous` and `page.next` variables which you can use get the title and
url of those pages. Hence, in `_layouts/post.html`:

{% raw %}
```liquid
<div class="page-navigation">
  {% if page.previous.url %}
    <div class="prev">
      <a href="{{ page.previous.url }}">&laquo; {{ page.previous.title }}</a>
    </div>
  {% endif %}
  {% if page.next.url %}
    <div class="next">
      <a href="{{ page.next.url }}">{{ page.next.title }} &raquo;</a>
    </div>
  {% endif %}
</div>
```
{% endraw %}

And some styling in my `assets/main.scss`:

```scss
.page-navigation {
    .next, .prev {
        display: inline-block;
        width: 45%;
    }
    .next {
        text-align: right;
        float: right;
    }
}
```
