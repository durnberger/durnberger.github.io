---
layout: post
title: Jekyll Excerpts
date: 2020-10-21
categories: jekyll
tags: [excerpts, liquid]

---
How to control the use and placement of excerpts within documents.

<!--more-->

When using Jekyll, the blog index page can be configured to show each post in full, achieved with the command `{% raw %}{{ post.content }}{% endraw %}` To show only an excerpt, the command is `{% raw %}{{ post.excerpt }}{% endraw %}`.

By default, if `{% raw %}{{ post.excerpt }}{% endraw %}` is used, Jekyll will show the first paragraph of every post. This may suit your needs, but there may be occasions when a post is short, and the use of an excerpt is pointless.

<!--more-->

To provide you with more control as to whether an excerpt is used, and if so where in the document it appears, do as follows.

We begin by overriding Jekyll's default setting; add the following to `_config.yml`

```yaml
# Excerpt Separator
excerpt_separator: <!--more-->
```

Next, add the following code to `index.html`, or whichever page you use to display your list of posts.

```liquid
{% raw %}{% if post.excerpt != post.content %}
<a class="read-more" href="{{ site.baseurl }}{{ post.url }}">[Read more...]</a>
{% endif %}{% endraw %}
```

Now go to one of your posts, and insert `<!--more-->` wherever you want the excerpt to end. View the saved post in your browser and you will find the excerpt ends with a `read-more` link. Click on it to view the whole document.

Thanks go to [MuffinMan](https://muffinman.io/jekyll-read-more-link/) who came up with this solution.
