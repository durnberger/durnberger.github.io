---
layout: page
permalink: /
---

Welcome to My Home Page

{% assign date = '2020-04-13T10:20:00Z' %}

- Original date - {{ date }}
- With timeago filter - {{ date | timeago }}




<div id="archive">

  <h2>Archive</h2>

  <div class="archive-cats">
    <h3 id="categories">Topics</h3>
    {% assign categories = site.categories | sort %}
    <p>
    {% for category in categories %}
        <a class="archive-cats-cat" href="/category/{{ category | first | slugify | downcase }}/">{{ category[0] | capitalize | replace: '-', ' ' }}</a>
    {% endfor %}
    </p>
  </div>

  <div class="archive-tags">
    <h3 id="tags">Tags</h3>
    {% assign tags = site.tags | sort %}
    <p>
    {% for tag in tags %}
      <a class="hashtags" href="/tag/{{ tag | first | slugify }}/">#{{ tag[0] | replace:'-', ' ' }}</a>
    {% endfor %}
    </p>
  </div>

  <div class="archive-posts">

    <h3 id="posts">Posts</h3>

    {% assign postsByYearMonth = site.posts | group_by_exp:"post", "post.date | date: '%B %Y'"  %}

    {% for yearMonth in postsByYearMonth %}

      <table id="table">

        <th colspan="3">{{ yearMonth.name }}</th>

        {% for post in yearMonth.items %}

          <tr>
            <td class="published">{{ post.date |  date: '%d %b %Y' }}</td>

            <td class="link"><a href="{{ post.url }}">{{ post.title | escape }}</a></td>

            <td class="excerpt">{{ post.excerpt | escape }}</td>
          </tr>

        {% endfor %}

      </table>

    {% endfor %}
  </div>

</div><!--end of #archives-->
