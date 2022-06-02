---
layout: post
title: Markdown Editor
date: 2020-10-14
categories: markdown
tags: [atom, packages]

---

A brief article explaining how to set up Atom as a markdown editor.

<!--more-->

My preferred markdown editor is [Atom](https://atom.io). Once it has been installed, I would recommend adding the following plugins from the Atom repository.

Recommended Plugins;
1. markdown-writer by zhuochun
2. toolbar-markdown-writer by zhuochun
3. wordcount by nesQuick
4. markdown-to-pdf by jooola
5. spell-check by atom

With regards spell-check, you may need to add `text.md` at `packages/spell-check/settings/grammars` before the spellchecking works.

To see a preview of your markdown document, use `ctrl-shift-m`. The preview will appear in a separate panel.

To convert the markdown file to html, right click anywhere in the preview pane, and select `Save as HTML...`.

To convert the document to a PDF, from the menu bar select `Packages > Markdown to PDF > Convert` or use the keyboard combination `ctrl-alt-e`.
