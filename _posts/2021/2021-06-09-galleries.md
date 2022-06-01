---
layout: post
title: Galleries
categories:
  - jekyll
  - photography
tags:
  - gallery
  - liquid
excerpt:
  How creating a new gallery framework can be made a little easier using jekyll and liquid.

---

As you might expect from a photographer's blog, my posts will often include collections of pictures. Creating a new gallery framework for each new post was becoming tedious, but thanks to the versatility of jekyll and liquid, there is a way to make the task a little easier, and this is how I did it.

Below is an example of the frontmatter used in one of my gallery posts;

```liquid
{% raw %}---
layout: post
title: Pushing Film
categories: photography
tags: [35mm, analogue, pushing, seasons, spring]

images:
  - image-path: 2021-06-07/001.jpg
    cols: col-sm-12
    title: Knightwood

  - image-path: 2021-06-07/002.jpg
    cols: col-sm-6
    title: Knightwood

---{% endraw %}
```

Within the body of post, and at the location where I want the pictures to appear, I have added `{% raw %}{% include gallery.html %}{% endraw %}`. The file to which this line refers, `_includes/gallery.html`, is comprised of the following;

```html
{% raw %}<div class="row g-1">

  {% for item in page.images %}
    <div class="{{ item.cols }}">

      <a href="/assets/images/{{ item.image-path }}" data-lightbox="gallery" data-title="{{ item.title }}">

      <img src="/assets/images/{{ item.image-path }}" alt="{{ item.title }}"/>

      </a>

    </div>
  {% endfor %}

</div><!--End of row-->{% endraw %}
```

I utilise Bootstrap to configure this website, and the `cols` (or columns) referred to in the frontmatter are as defined by Bootstrap. Likewise I use a lightbox, hence the `data-lightbox` and `data-title` elements within `gallery.html`.

As you will appreicate, `{% raw %}{% include gallery.html %}{% endraw %}` can be added to any post where you want a collection of pictures to appear. All you need do is include within the post's frontmatter a list of the pictures to be used; it really is that simple!
