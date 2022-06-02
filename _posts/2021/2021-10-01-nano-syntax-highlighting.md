---
layout: post
categories:
  - linux
  - markdown
tags:
  - nano
  - syntax

---
Syntax highlighting for markdown files in nano.

<!--more-->

This post explains how to add syntax highlighting for markdown files in nano.

Referring to the file `~/.nanorc`, ensure the line `include "/usr/share/nano/*.nanorc"` is uncommented.

Create a new file, `sudo nano /usr/share/nano/markdown.nanorc`,
and add the following to it.

```
syntax "markdown" "\.md$" "\.markdown$"

## Quotations
color cyan "^>.*"

## Emphasis
color green "_[^_]*_"
color green "\*[^\*]*\*"

## Strong emphasis
color brightgreen "\*\*[^\*]*\*\*"
color brightgreen "__[\_]*__"

## Underline headers
color brightblue "^====(=*)"
color brightblue "^----(-*)"

## Hash headers
color brightblue "^#.*"

## Linkified URLs (and inline html tags)
color brightmagenta start="<" end=">"

## Links
color brightmagenta "\[.*\](\([^\)]*\))?"

## Link id's:
color brightmagenta "^\[.*\]:( )+.*"

## Code spans
color brightyellow "`[^`]*`"

## Links and inline images
color brightmagenta start="!\[" end="\]"
color brightmagenta start="\[" end="\]"

## Lists
color yellow "^( )*(\*|\+|\-|[0-9]+\.) "

```

Syntax highlighting for a variety of other file types can be found [here](https://github.com/serialhex/nano-highlight).
