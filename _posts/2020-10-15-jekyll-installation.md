---
layout: post
title: Jekyll Installation
date: 2020-10-15
categories: jekyll
tags: [gems, installation]

---
It would be so much easier to upload HTML documents as they are, and have them converted on the fly. Jekyll provides the solution.

<!--more-->

Instead of converting markdown documents into HTML format, it would be so much easier to upload the documents as they are, and have them converted on the fly. One such system, and one I have wanted to try for some time is [Jekyll](https://jekyllrb.com/). As explained on their website, it is simple.

> No more databases, comment moderation, or pesky updates to install—just your content.

With my new Linux install up and running, it was now time to give it a whirl.

### Installation
Following the guide on the Jekyll website, the basic installation was straightforward. Enter the following commands using your favourite terminal;

```
gem install bundler jekyll
jekyll new my-awesome-site
cd my-awesome-site
bundle exec jekyll serve
```

The newly created webpage can then be viewed in your browser at

```
http://localhost:4000
```

The guide at the Jekyll website also explains how to set up your index page,the first post, and so forth.
