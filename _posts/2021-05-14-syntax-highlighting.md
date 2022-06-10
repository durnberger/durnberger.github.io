---
layout: post
title: Syntax Highlighting
date: 2021-05-14
categories: jekyll
tags: [rouge, syntax]

---
Using Rouge, Jekyll's default syntax highlighter.

<!--more-->

Syntax highlighters are used to highlight text and code snippets. Rouge is the default highlighter used by Jekyll.

Begin by installing the `rouge` gemfile

```bash
gem install rouge
```
There are a number of syntax themes available (a list of which can be found [here](https://github.com/rouge-ruby/rouge/tree/master/lib/rouge/themes)).

To generate the `.scss` file for a particular theme, in this case gruvbox, use the following command;

```bash
rougify style gruvbox > _sass/syntax.scss
```

To incorporate the syntax style into your web site, add the following line to `/assets/css/main.css`;

```bash
@import "syntax" ;
```
