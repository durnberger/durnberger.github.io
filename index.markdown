---
layout: page
permalink: /
---

<div id="archive">

  <div class="archive-posts">

    <h2 id="posts">Posts</h2>

    {% assign postsByYearMonth = site.posts | group_by_exp:"post", "post.date | date: '%B %Y'"  %}

    {% for yearMonth in postsByYearMonth %}

      <div class="yearmonth">

        <h3>{{ yearMonth.name }}</h3>

        {% for post in yearMonth.items %}

          <div class="entry">

            <div class="link"><a href="{{ post.url }}">{{ post.title }}</a></div>

            <div class="excerpt">{{ post.excerpt | strip_html }}</div>

          </div>

        {% endfor %}

      </div><!--End of yearmonth-->

    {% endfor %}
  </div><!--end of archive-posts-->

</div><!--end of #archives-->
