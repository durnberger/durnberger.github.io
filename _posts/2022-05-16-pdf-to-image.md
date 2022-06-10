---
layout: post
categories: [linux]
tags: [jpeg, pdf, png]

---
How to convert a PDF into image file(s).

<!--more-->

This can be achieved using `pdftoppm`, a part of the `poppler-utils` package.

To convert a PDF to a PNG:

```
pdftoppm input.pdf outputname -png
```

To convert a PDF to a JPEG:

```
pdftoppm input.pdf outputname -jpeg
```
