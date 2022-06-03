---
layout: page
permalink: /
---

<div id="archive">

  <div class="archive-posts">

    <h2 id="posts">Posts</h2>

    {% assign postsByYearMonth = site.posts | group_by_exp:"post", "post.date | date: '%B %Y'"  %}

    {% for yearMonth in postsByYearMonth %}

      <h3 class="yearmonth">{{ yearMonth.name }}</h3>

      {% for post in yearMonth.items %}

        <div class="entry">

          <div class="link"><a href="{{ post.url }}">{{ post.title }}</a></div>

          <p class="excerpt">{{ post.date |  date: '%d %B %Y' }} - {{ post.excerpt | strip_html }}</p>

        </div>

      {% endfor %}

    {% endfor %}
  </div>

</div><!--end of #archives-->
