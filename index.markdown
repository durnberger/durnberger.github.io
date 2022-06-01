---
layout: page
permalink: /
---

<div id="archive">

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
