---
layout: post
title: Add pagination to index of blog posts
category: metablogging
tags: [jekyll]
---

Another feature I wanted to add to this blog - pagination on the posts index.
Here's Jekyll's documentation on pagination:
<https://jekyllrb.com/docs/pagination/>

But I found this blog post more helpful, which walks you through setting it up
in more detail:
<https://blog.webjeda.com/jekyll-pagination/>

You need to enable the jekyll-paginate plugin in \_config.yml, like this:

```ruby
plugins: [jekyll-paginate]
```

and also in the Gemfile. Pagination settings are set in \_config.yml like this:

```ruby
paginate: 8 # number of posts per page
paginate_path: "/page:num/" # index pages will appear at /page2/, /page3/ etc
```

You can then loop through the posts and get links to the next and previous index
pages using the `paginator` variable. To see how that works [check out the 
index.html page from the relevant commit to the repo][index-page-with-pagination].

I think the blog is basically useable now, but what else do I still want to add?
- I didn't add a category page before, but I'm thinking it might actually be
useful since I'm using categories to distinguish posts about Makers stuff and
stuff about this blog
- Some sort of javascript-based client-side search function?

[index-page-with-pagination]:https://github.com/Hives/hives.github.io/blob/aa331c692fe0ad74b9aa8db9955ccb35a5bc881b/index.html

