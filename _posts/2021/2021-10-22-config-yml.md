---
layout: post
categories: jekyll
tags: [configuration]
excerpt:
  An example of the `_config.yml` file as used within a Jekyll configuration.
---

When using the *Jekyll Static Site Generator*, it is essential for `_config.yml` to be properly configured. The example below worked for me, and I leave it here just in case it provides some assistance to anyone struggling to get their own project up and running.

```
# Global Settings
title: Site Title
author: Site Author
description:
  A description of the your site.

keywords:
  atom, bootstrap, css, html, github, git, jekyll, linux, markdown, technology, ubuntu

baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com

# Build settings
permalink: /:year/:month/:day/:title/

plugins:
  - jekyll-feed
  - jekyll-paginate-v2

sass:
  sass_dir: _sass
  style: compressed

include: ['_pages']

markdown: kramdown

kramdown:
  input: GFM
  syntax_highlighter: rouge

# Plugin: Pagination (jekyll-paginate-v2)
pagination:
  enabled: true
  per_page: 8
  permalink: '/page:num/'
  title: ':title-page :num'
  limit: 0
  sort_field: 'date'
  sort_reverse: true

# Plugin: Auto Pages (jekyll-paginate-v2)
autopages:
  enabled: true

  collections:
    enabled: false

  categories:
    enabled: true
    layouts:
      - 'category.html'
    title: ":category"
    path: "/category/:category"

  tags:
    enabled: true
    layouts:
      - 'tag.html'
    title: ':tag'
    path: '/tag/:tag'

# Excerpt Separator
excerpt_separator: <!--more-->

# Files to Ignore on Build
keep_files: ['.jpg', '.jpeg', '.gif', '.pdf']

# Exclude from Processing.
# The following items will not be processed, by default.
# Any item listed under the `exclude:` key here will be automatically added to
# the internal "default list".
#
# Excluded items can be processed by explicitly listing the directories or
# their entries' file path in the `include:` list.
#
exclude:
  - Gemfile
  - Gemfile.lock
  - .sass-cache/
  - .jekyll-cache/
  - gemfiles/

#  - node_modules/
#  - vendor/bundle/
#  - vendor/cache/
#  - vendor/gems/
#  - vendor/ruby/
```
