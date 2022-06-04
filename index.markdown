---
layout: page
permalink: /
---
<div id="archive">

  <h2 id="posts">Posts</h2>

  {% for post in site.posts %}

    {% include entry.html %}

  {% endfor %}

</div><!--end of #archives-->
