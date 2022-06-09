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
syntax "Markdown" "\.(md|mkd|mkdn|markdown)$"

# Tables (Github extension)
color cyan ".*[ :]\|[ :].*"

# quotes
color brightyellow  start="^>" end="^$"
color brightyellow  "^>.*"

# Emphasis
color green "(^|[[:space:]])(_[^ ][^_]*_|\*[^ ][^*]*\*)"

# Strong emphasis
color brightgreen "(^|[[:space:]])(__[^ ][^_]*__|\*\*[^ ][^*]*\*\*)"

# strike-through
color red "(^|[[:space:]])~~[^ ][^~]*~~"

# horizontal rules
color brightmagenta "^(---+|===+|___+|\*\*\*+)\s*$"

# headlines
color brightred  "^#{1,6}.*"

# lists
color cyan   "^[[:space:]]*[\*+-] |^[[:space:]]*[0-9]+\. "

# leading whitespace
color black    "^[[:space:]]+"

# misc
color magenta   "\(([CcRr]|[Tt][Mm])\)" "\.{3}" "(^|[[:space:]])\-\-($|[[:space:]])"

# links
color brightblue "\[[^]]+\]"
color brightblue "\[([^][]|\[[^]]*\])*\]\([^)]+\)"

# images
color magenta "!\[[^][]*\](\([^)]+\)|\[[^]]+\])"

# urls
color brightyellow "https?://[^ )>]+"

# code
color yellow   "`[^`]*`|^ {4}[^-+*].*"
# code blocks
color brightyellow start="^```[^$]" end="^```$"
color brightyellow "^```$"

## Trailing spaces
color ,green "[[:space:]]+$"

```

Syntax highlighting for a variety of other file types can be found [here](https://github.com/serialhex/nano-highlight).
