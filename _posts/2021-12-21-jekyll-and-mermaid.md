---
layout: post
categories: jekyll
tags: [graphics, mermaid]

image1:
  - file_path: /assets/graphics/2021-12-21-mermaid1.png
    caption: Mermaid Graphic
    cols: col-12

image2:
  - file_path: /assets/graphics/2021-12-21-mermaid2.png
    caption: Flyout Panel
    cols: col-12

---
Using Mermaid to create graphs for use in your Jekyll project.

<!--more-->

Over many years I have been working on my family history. I'm presently creating a website, which will bring together a collection of biographies detailing what I have learnt about the lives of my forebears.

To make it easier for the reader to understand the connection between those forebears and the present generation, I wanted to create family trees illustrating the links. What I needed was a programme that would allow me to easily create a graph or flow diagram; in my quest to find something suitable, I discovered [Mermaid](https://mermaid-js.github.io/mermaid/#/){:target="_blank"}.

### Setting Up
I was able to generate graphs using the following technique;

Add the following to `_layouts/default.html`, at a point just before the `</body>` tag.

```java
<script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

<script>mermaid.initialize({ startOnLoad: true });</script>
```

Add `jekyll-mermaid` to the plugins section of `_config.yml`

Add `gem "jekyll-mermaid"` to the `gemfile`.

Run `bundle exec jekyll serve --livereload` and rebuild the project.

With everything in place, open a new markdown file, enter the following;

```
{% raw %}<div class="mermaid">
graph TD
  A --> B;
  A --> C;
  A --> D;
</div>{% endraw %}
```

Having saved the document, and once the project has finished rebuilding, you will have a graph that looks something like this;

{% include images.html content=page.image1 %}


Impressive. A *family tree* layout any genealogist would find useful!

However, the tree is generated when the page is called, which to my mind does rather defeat the point of a static web site. If you would rather create an image of the graph before it is uploaded to the server, and if you are using the Atom Editor, here is an alternative you can try.

### The Alternative
We do not need to add the javascript to the body, or to add the reference to `jekyll-mermaid` in `_config.yml` or the `gemfile`.

Instead, in the Atom Editor, go to [Edit > Preferences > Install ]. Search for `atom-mermaid`, and install it.

Create a new file, and add just the code needed to generate the graph

```
graph TD
  A --> B;
  A --> C;
  A --> D;
```

Right click on the code, and from the fly out panel, click on `mermaid preview`. Run the mouse over to the preview produced and again right click, and this time either `Save as PNG` or `Save as SVG`.


{% include images.html content=page.image2 %}


You will be asked where to save the image (in my case they go into `/assets/media/graphics`). The image is now ready to be used.

### Layout
I have created a template, `_layouts/biography.html`, which as you might expect is the layout I use when creating a new biography page. Within it I have added;

```html
{% raw %}{% if page.tree == true %}
  <h3>Relationships</h3>

  <div class="tree thumbnail">
    <img src="/assets/media/trees/{{ page.title | replace: ' ', '-' | downcase }}.png" class="img-fluid" alt="{{ page.title }}">
  </div>

{% endif %}{% endraw %}
```

Provided the frontmatter for the biography I am writing includes the line `tree: true`, then the requisite tree will be dropped into the newly created page. This will work as long as the title of the biography page matches the filename for the associated graphic. So for example, I have created a biography page describing my grandfathers life. The front matter appears as follows;

```liquid
{% raw %}---
layout: biography
title: My Grandfather

categories: biographies
tags: [associated, surnames]

tree: true
---{% endraw %}
```

Note the title; the graphic, showing my grandfather's family tree, needs to be saved as `/assets/media/trees/my-grandfather.png`

Once the biography page has been saved and the project rebuilt, you should find the graphic displayed in all its glory!
