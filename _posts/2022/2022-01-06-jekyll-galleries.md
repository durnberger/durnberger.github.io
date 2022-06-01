---
layout: post
categories: jekyll
tags: [gallery, liquid, website]
excerpt:
  How to create galleries for your Jekyll project

---

I wanted to display a gallery of old family photographs on my genealogy website. I have come up with two solutions, detailed below.

I utilise Bootstrap. The code detailed below includes reference to Bootstrap elements; those elements can be removed without affecting the basic functionality of these solutions.

### Solution 1
#### 1.1 The Includes File
Create a new file `_includes/gallery.html`. Paste in the following code;

```html
{% raw %}<div id="gallery">
  <div class="row g-1">
    {% for image in site.static_files %}
      {% if image.path contains include.folder %}
        <div class="{{ page.cols }}">
          <div class="thumbnail">
            <div class="ratio ratio-1x1">
              <a href="{{ site.baseurl }}{{ image.path }}" data-lightbox="gallery" data-title="{{ image.file }}"><img src="{{ site.baseurl }}{{ image.path }}" class="img-fluid img-thumbnail" alt="{{ image.file }}"></a>
            </div><!--End of ratio-->
          </div><!--End of thumbnail-->
        </div><!--End of col-*-->
      {% endif %}
    {% endfor %}
  </div><!--End of row-->
</div><!--End of #gallery-->{% endraw %}

```

#### 1.2 Saved Photographs
Next, save the photographs to be used in the gallery to the `assets` directory. In my case I have saved them in the directory `/assets/images/family`

#### 1.3 The Post
Now create a post. The front matter would need to include reference to the `family` album in which the photographs have been saved;

```liquid
{% raw %}---
layout: post
album: family

cols: 'col-sm-4'
---{% endraw %}
```
Within the body of the post, and at the point where you want the gallery to appear add the following;

```liquid
{% raw %}{% include gallery.html folder="family" %}{% endraw %}
```

#### 1.4 Conclusion
All of the photographs in the `family` directory will be displayed in the gallery. Thanks to the settings in the `frontmatter`, each thumbnail will be the same proportion and will occupy the same space on the page. This will look fine until you get to the last picture, which may be sitting on its own on the last line.

What if you want more control over the width of each thumbnail, and the space each occupies on the page? The following solution might help.

### Solution 2
#### 2.1 The Includes File
Create a new file `_includes/gallery.html`. Paste in the following code;

```html
{% raw %}<div id="gallery">
  <div class="row g-1">
    {% for item in page.pictures %}
      <div class="{{ item.cols }}">
        <div class="thumbnail">
          <div class="ratio ratio-1x1">
            <a href="/assets/images/{{ page.album }}/{{ item.file }}" data-lightbox="gallery" data-title="{{ item.file }}"><img src="/assets/images/{{ page.album }}/{{ item.file }}" class="img-fluid img-thumbnail" alt="{{ item.caption }}"></a>
          </div>
        </div><!--End of thumbnail-->
      </div><!--End of col-*-->
    {% endfor %}
  </div><!--End of row-->
</div><!--End of #album-->{% endraw %}
```

#### 2.2 The Post
Now create a post. The front matter again needs to include reference to the relevant album. In addition we need to refer to each photograph, detailing the file name and the proportion of the page width it should occupy.

The `col-*` element is used by Bootstrap, which divides the page into 12 imaginary columns. The value `col-4` means the photograph will occupy 4/12 of the page width.

```liquid
{% raw %}---
layout: post
album: family

pictures:
  - file: 001.jpg
    cols: 'col-sm-4'

  - file: 002.jpg
    cols: 'col-sm-4'

  - file: 003.jpg
    cols: 'col-sm-4'

  - file: 004.jpg
    cols: 'col-sm-12'
---{% endraw %}
```

In this example, the first three pictures are each assigned a column width of 4/12 of the body width, meaning the first three pictures will sit tidily together on the first row. However the fourth picture, if assigned a width of `col-4` would also occupy just a third of the body width. Too untidy for my liking, so instead we assign it a value of `col-12`. That final picture will now occupy the full width of the bottom row. Nice.

Finally, add the following code to wherever in the post you want the album to appear;

```liquid
{% raw %}{% include gallery.html %}{% endraw %}
```

#### 2.3 Conclusion
The only drawback with this solution is that you have to make reference to every picture in the album in the front-matter, which could be tiresome if there are a lot of pictures. I wonder if there is some way to combine the two options so as to take the drudgery out of solution 2?
