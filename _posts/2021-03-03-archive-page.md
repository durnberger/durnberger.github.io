---
layout: post
title: Archive Page
date: 2021-03-03
categories: jekyll
tags: [archives, categories, liquid, tags]

---
How to create an archive page that lists all posts according to the year and month of publication.

<!--more-->

I have modified my archive page, so that now all posts are listed according to the year and month of publication. In addition, any categories or tags used in those posts will be automatically listed.

I also realise that using this method, one does not need to use the jekyll plugin, `jekyll-archives`, and I have removed it from my site.

<!--more-->

### Contents
{% include toc.html %}

### Categories
```html
{% raw %}<div id="archive-cat">
  <h2>Categories</h2>
    <ul>
      {% for category in site.categories %}
      {% assign category_name = category[0] %}
        <li>
          <a href="/category/{{ category_name | slugify }}/">{{ category_name | replace: "-", " " }}</a>
        </li>
      {% endfor %}
    </ul>
</div><!-- End of #archive-cat -->{% endraw %}
```

### Tags
```html
{% raw %}<div id="archive-tag">
  <h2>Topics</h2>
    <ul>
      {% assign tags = site.tags | sort %}
      {% for tag in tags %}
        <li>
          <a href="/tag/{{ tag | first | slugify }}/">{{ tag[0] | replace:'-', ' ' }}</a>
        </li>
      {% endfor %}
    </ul>
</div><!-- End of #archive-tag -->{% endraw %}
```
### Month & Year
```html
{% raw %}<div id="archive-month">
  <h2>Articles</h2>
    {% assign postsByYearMonth = site.posts | group_by_exp:"post", "post.date | date: '%Y %B'"  %}
    {% for yearMonth in postsByYearMonth %}
      <h3>{{ yearMonth.name }}</h3>
        <ul>
          {% for post in yearMonth.items %}
            <li><a href="{{ post.url }}">{{ post.title }}</a></li>
          {% endfor %}
        </ul>
          {% endfor %}
</div><!-- End of #archive-month -->{% endraw %}
```
