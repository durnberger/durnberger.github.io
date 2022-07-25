---
title: Nano Configuration
layout: post
categories: linux
tags:
  - nano
---

### ~/.nanorc

```
# Syntax Highlights
include "/usr/share/nano/*.nanorc"

# Options
set tabsize 2
set tabstospaces
set autoindent
set trimblanks
set linenumbers
set constantshow
set titlecolor red,white
set keycolor black,white  # colors in the help panel
set functioncolor white   # colors in the help panel
set numbercolor yellow
set mouse           # enable mouse support
set smarthome       # `Home` jumps to line start first
set afterends       # `Ctrl+Right` move to word ends instead of word starts
set wordchars "_"   # recognize '_' as part of a word
set softwrap

# Keybindings
unbind ^C main
unbind ^X main
unbind ^V main
unbind ^K main
unbind ^S main
unbind ^Q main

bind ^C   copy          main
bind ^X   cut           main
bind ^V   paste         main
bind ^K   zap           main  # deletes all selected text
bind ^S   writeout      all   # save file
bind ^Q   exit          all

```

### Markdown Syntax Highlighting

```
syntax "markdown" "\.md$" "\.markdown$"

## Quotations
color yellow "^>.*"

## Emphasis
color brightmagenta "_[^_]*_"
color brightmagenta "\*[^\*]*\*"

## Strong emphasis
color brightgreen "\*\*[^\*]*\*\*"
color brightgreen "__[\_]*__"

## Underline headers
color brightblue "^====(=*)"
color brightblue "^----(-*)"

## Hash headers
color brightblue "^#.*"

## Linkified URLs (and inline html tags)
color brightblue start="<" end=">"

## Links
color brightblue "\[.*\](\([^\)]*\))?"

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
