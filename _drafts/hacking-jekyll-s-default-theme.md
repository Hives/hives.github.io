---
layout: post
title: Hacking Jekyll's default theme
category: metablogging
tags: [jekyll, liquid]
---

I wanted to make some changes to the look of my (this) Jekyll blog. Nothing too
outré. Helpfully, Minima, the Jekyll default theme, has a README file with information
about customising it. I'm not using the most up to date version of Minima (maybe
because the github-pages gem requires an older version of Jekyll?), so here's
the relevant version of the README for my site:

<https://github.com/jekyll/minima/blob/v2.5.0/README.md>

I started by running `bundle show minima` to find the location of the theme on
my system. Customising then consisted of copying relevant template files into
the right location in my Jekyll site, and editing them. If the files exist in
the local folder Jekyll will use those in preference to the original versions in
the theme folder.

I added my own Sass rules by copying Minima's `main.scss` into
`<my-site>/assets` and putting my code below the `@import "minima";` line.

## Tags and Categories

First up, since I've been fastidiously tagging all my posts since I started
blogging, I wanted to actually use the tags on the site. I wanted to display
them on post pages, and also create a "Tags" page. Ditto for categories.

### Display tags and categories on post pages

To get tags on my post pages I created a `_layouts` folder in the root folder of
my site, copied `post.html` into it from the Minima gem folder, and added this
beneath the post content:

{% raw %}
```liquid
<div class="tags-and-categories">
  <span class="post-tags">
  {% if page.tags.size > 0 %}
    Tags: {% for tag in page.tags %}
      <a href="/tags/{{ tag }}/">{{ tag }}</a>
      {%- unless forloop.last -%}
        ,
      {%- endunless %}
    {% endfor %}
  {% else %}
    This post does not have any tags
  {% endif %}
  </span>
</div>
```
{% endraw %}

I added the equivalent code for categories in the same place too. This creates a
comma-separated list of links to the relevant tag pages. These don't exist at
the moment, so I'll be coming back to that...

The `forloop.last` part is an example of a Liquid *helper variable*.

> During every `for` loop the following variables are available for extra
> styling needs:
> 
> ```liquid
> forloop.length      # => length of the entire for loop
> forloop.index       # => index of the current iteration
> forloop.index0      # => index of the current iteration (zero based)
> forloop.rindex      # => how many items are still left?
> forloop.rindex0     # => how many items are still left? (zero based)
> forloop.first       # => is this the first iteration?
> forloop.last        # => is this the last iteration?
> ```

From [Liquid for
designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers) on the
Liquid GitHub, lots of other good stuff there.

This let me avoid adding a comma after the last list item.

{% raw %}
Note also the hyphens in some of the liquid tags: `{%-` and `-%}`. This removes
the whitespace which is otherwise generated either side of the output, so the
commas appear next to the tags without a space.
{% endraw %}

For styling, I copied Minima's Sass rule for the `.post-meta` selector and
applied it to `.tags-and-categories` in my `assets/main.scss`:

```scss
.tags-and-categories {
  font-size: $small-font-size;
  color: $grey-color;
}
```


