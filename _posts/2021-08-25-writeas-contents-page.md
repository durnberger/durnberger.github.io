---
layout: post
categories:
  - jekyll
tags:
  - theme
  - writeas

---

How I created a contents page for my *write.as* blog.

<!--more-->

I tend to write my posts using the [Atom text editor](https://atom.io/), before then copying the completed work into *write.as*.

In the past I have created a number of web sites from scratch, writing the content using Atom, but generating the finished web site using [Jekyll](https://jekyllrb.com/). Jekyll is open source, and free to use. It can be [installed](https://jekyllrb.com/docs/installation/) on Windows, macOS and Linux. But what, you might ask, has that got to do with posting to *write.as*?

One of the disadvantages of *write.as* is that it does not generate a separate contents page of the type you might have found useful when blogging with *WordPress*. Utilizing *Jekyll* provides a means of circumventing this problem, and creating a contents page that is easy to maintain. The following explains how to go about it.

### Create a New Jekyll Project
Begin by installing Jekyll, as per [Jekyll's quick start instructions](https://jekyllrb.com/), then create your first project using the following command;

`jekyll new my-new-project`

CD into the directory `my-new-project`, and you will find a number of directories, including one called `_posts`. As you might expect it is within this directory you save your posts.

### The First Post
CD into `_posts` and create a new markdown file. This *must* be named using the format `yyyy-mm-dd-post-title.md`. Let's assume we have created a new file called `2021-08-23-new-post.md`. Open it and add three dashes each to the first and second lines. This is called the `frontmatter`;

```
---
---
```

**The `frontmatter` must be correctly formatted. Ensure there are two lines each comprising three dashes as shown; if they are not present the process described below will not work.**

Write your post, so that you have a document laid out in the following fashion.

Note that we saved our file as `2021-08-23-new-post.md`. The title of the post must match, so in this case we see `New Post` just below the `frontmatter`.

```
---
---

# New Post
This is the post content

#tag1 #tag2 #tag3

```

Once you have completed your post, copy everything below the `frontmatter` and paste it into a new post in *write.as*, and publish it.

### Index.markdown
Return to the directory `my-new-project` and find the file named `index.markdown` Replace the content with the following and save it.

**The `frontmatter` must be correctly formatted. Ensure there are three dashes each on the first two lines; if they are not present the process described will not work**

Also, don't forget to change `[your-blog-title]` to your blog title!

```
{% raw %}---
---
{% assign sorted = site.posts | sort: 'date' | reverse %}
{% for post in sorted %}
{{ post.date | date: '%d %b %Y' }}: <a href="https://write.as/[your-blog-title]/{{ post.title | replace: ' ', '-' | downcase }}">{{ post.title }}</a>
{% endfor %}{% endraw %}
```

### Jekyll Serve
Open a terminal window and CD into the `my-new-project` directory. Next, type the following command and hit return;

`bundle exec jekyll serve`

Wait for a few moments until a line of text stating `done in x.xxx seconds` or similar appears. Now refer back to the `my-new-project` directory, and the folder `_site`. Open the document `index.html`, and there you will see a list of your posts, with the date and title of each post, constrained by elements of HTML.

**Note that the content of `_site` will be re-written every time `bundle exec jekyll serve` is run.**

Copy the content of `_site/index.html`

Now go to *writeas* and paste what you have just copied into a new post. Remember to give this new post a title as you would any other; *content* is as good a title as any. Publish it, and then pin it so it appears as a menu item at the top of the page. Now you have a page that lists all of your *write.as* posts, and with a link to each post.

The post titles that appear on the contents page are drawn from the posts filename. So in our example, we named the new file `2021-08-25-new-post.md`, and so the posts title that appears in `_site/index.html` would be *New Post*. When copying the post into *write.as* you would need to ensure the *write.as* post is also entitled *New Post*. If this isn't done then the links generated for the contents page will not work.

### Example
The posts section on my [Archive](/) page shows what can be achieved. The layout was controlled using a table, as detailed in the script below;

```
{% raw %}---
---
<table>
  <tr>
    <th>Date</th>
    <th>Title</th>
  </tr>
  {% assign sorted = site.posts | sort: 'date' | reverse %}
  {% for post in sorted %}
  <tr>
    <td>{{ post.date | date: '%d %b %Y' }}</td>
    <td><a href="https://write.as/[your-blog-title]/{{ post.title | replace: ' ', '-' | downcase }}">{{ post.title }}</a></td>
  </tr>
  {% endfor %}
</table>
```{% endraw %}

### Issues
1. Your existing posts will need to be modified to include the `frontmatter`

2. Remember to check that the post title assigned by *write.as* is **identical** to the file name assigned to the post when creating it in your text editor, else the links in your *write.as* contents page will not work.

3. Having written a new post in your text editor, you must then always
  + Run `bundle exec jekyll serve`
  + Copy and paste the new post into a new post on *write.as*
  + Copy and paste the refreshed version of `_site/index.html` into your *write.as* contents page.

### Conclusion
Whilst this process does require a little work at the outset, if you have a lot of *write.as* posts you want to index, I have found it is worth the effort. It is certainly a lot easier than trying to create an index manually.
