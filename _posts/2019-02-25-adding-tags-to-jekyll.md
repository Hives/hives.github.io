---
layout: post
title: Adding tags to my Jekyll site
date: 2019-02-25 00:11 +0000
category: metablogging
tags: [jekyll, liquid]
---

I wanted to add some features to my (this) Jekyll blog. Nothing too outré - a
tags page, next/previous post links, pagination on the list of posts. Helpfully,
Minima, the Jekyll default theme, has a README file with information about
customising it. I'm not using the most up to date version of Minima (maybe
because the github-pages gem requires an older version of Jekyll?), so here's
the correct README for the version I'm using:

<https://github.com/jekyll/minima/blob/v2.5.0/README.md>

I started by running `bundle show minima` to find the location of the theme on
my system. Customising then consisted of copying relevant template files into
the right location in my Jekyll site, and editing them. If the files exist in
the local folder Jekyll will use those in preference to the original versions in
the theme folder.

I added my own Sass rules by copying Minima's `main.scss` into
`<my-site>/assets` and putting my code below the `@import "minima";` line.

## Display tags (and categories) on post pages

To get tags on my post pages I created a `_layouts` folder in the root folder of
my site, copied into it the posts template `post.html` from the Minima gem
folder, and added this beneath the post content:

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

I added similar code for categories in the same place too. This creates a
comma-separated list of links to the relevant section of the tag page. The tag
page don't exist at the moment, so I'll be coming back to that...

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

## Create a tags page

It's easy to create a new page in Jekyll - I created a `tags.html` file in the
root directory and gave it some front matter:

{% raw %}
```html
---
layout: default
title: Tags
permalink: tags
---

<article class="tags">

  <header class="post-header">
    <h1 class="post-title">{{ page.title | escape }}</h1>
  </header>

</article>
```
{% endraw %}

This is then accessible at `mysite.com/tags` and it automatically appears in the
main menu.

I mostly took the code displaying the tag info from [this Jekyll theme's tag
page][codinfox-lanyon-tags-page]. It
works by iterating over the `site.tags` variable, like this:

{% raw %}
```liquid
{% for tag in site.tags %}
<h2>{{ tag[0] }}</h2>
<ul>
  {% for post in tag[1] %}
  <li>
    <a href="{{ site.baseurl }}{{ post.url }}">
    {{ post.title }}
    </a>
    <small class="post-date">({{ post.date | date_to_string }})</small>
  </li>
  {% endfor %}
</ul>
{% endfor %}
```
{% endraw %}
 
What wasn't easy however, was sorting the list of tags in a sensible way. I
wanted to make a sort of tag cloud, listing the name of the tag alongside the
number of posts using that tag, and make the tag's name link to a list of
tagged posts. And I wanted to sort the tags from most popular to least popular,
and alphabetically after that. Unfortunately this is hard to achieve in a
Liquid template, as you can't sort a hash of data.

[I found an ingenious workaround here][ingenious-workaround]. Instead of sorting
a hash, he put all the desired data into a long string separated by a special
character (he used `#`, I used `$`), so that he could later break it up into an
array, which you *can* sort in Liquid. It's not pretty but it works 😬. Using
this method I managed to get the tag cloud sorted in reverse order by popularity
(high to low), then alphabetically. You can see all the gory details [in the
GitHub repo for this site][tags-page-in-github].

A couple more styling rules in `assets/main.scss` and that was the tags page
finished. Once all that was sorted out I went back and updated the tags in
`_layouts/post.html` to link to the appropriate place on the tags page, like
this:

{% raw %}
```liquid
<a href="/tags#{{ tag | slugify }}">{{ tag }}</a>
```
{% endraw %}

[ingenious-workaround]:https://www.codeofclimber.ru/2015/sorting-site-tags-in-jekyll/
[tags-page-in-github]:https://github.com/Hives/hives.github.io/blob/1735a794a93dacfd74945814158495b55c1cf9e5/tags.html
[codinfox-lanyon-tags-page]:https://github.com/codinfox/codinfox-lanyon/blob/dev/blog/tags.html
