---
layout: post
title: Categories
categories: jekyll
tags:
  - categories
  - github
  - liquid

---
How to create a page to list posts by categories and which will work on GitHub Pages.

<!--more-->

For each category, create a page. Within the page, add the following script. In this example we are creating a page to display posts assigned to the category `jekyll`.

```liquid
<div id="category">
  <h2>CATEGORY: Jekyll</h2>

  {% raw %}{% for post in site.categories.jekyll %}{% endraw %}

    <div class="entry">

      {% raw %}<h3 class="link"><a href="{{ post.url }}">{{ post.title }}</a></h3>{% endraw %}

      {% raw %}<p class="excerpt">
        {{ post.date | date: '%d %B %Y' }}
          <br>
        {{ post.excerpt | strip_html }}
      </p>{% endraw %}

    </div>

  {% raw %}{% endfor %}{% endraw %}
</div>
```

With thanks to [qfimg.github.io](https://qfimg.github.io/jekyll-categories/){:target="_blank"}
