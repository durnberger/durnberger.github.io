---
layout: post
title: Jekyll and Liquid
date: 2020-10-18
categories: jekyll
tags: [liquid, raw]

---
How to display liquid coding within a code block.

<!--more-->

When writing posts about configuring Jekyll, I discovered that `liquid` coding would not appear within a code block. For example, below is a code block as it should appear.

```liquid
{% raw %}<div id="archives">
  {% for post in site.categories.category-name %}
   <li><span>{{ post.date | date: '%Y-%m-%d' }}</span> &nbsp; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</div>{% endraw %}
```

However, this is what was rendered;
```html
 <div id="archives">
  {% for post in site.categories.category-name %}
   <li><span>{{ post.date | date: '%Y-%m-%d' }}</span> &nbsp; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</div>
```

The problem arises because the tags within the code block are being processed. The solution? Add &#123;&#37; raw &#37;&#125; before the first line of the code block and &#123;&#37; endraw &#37;&#125; after the last line.
