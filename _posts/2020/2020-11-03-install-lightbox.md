---
layout: post
title: Install a Lightbox
date: 2020-11-03
categories: photography
tags: [html, liquid, website]
excerpt:
  I wanted a way to better display the images on this web site, and decided to utilize Lightbox.
---

I wanted a way to better display the images on my photography web site, and decided to utilize a lightbox. The idea is that when one clicks on the thumbnail of an image, a large version of the image appears, sitting over the main page. The lightbox I used on was installed as follows.

<!--more-->

I am using Lightbox2, a very light JavaScript application. As described at the [Lightbox2 web site](https://lokeshdhakar.com/projects/lightbox2/), one first needs to download the zip of the latest release. If using Linux, the files can be downloaded using the command;

```
npm install lightbox2 --save
```

If npm is not already installed on your system, use the following command to install it;

```
sudo apt-get install npm
```

Having downloaded lightbox2, navigate to the `lightbox2/src` folder, where you will find three further folders, `css,images` and `js`.

Now create a folder called lightbox within your web page structure (I have mine at /assets/lightbox). Copy the contents of `lightbox2/src` into the newly created folder.

Within the `<head>` section of your web page, add a link to the `lightbox.css` file. In my case this is;

 ```html
 <link href="/assets/lightbox/css/lightbox.css" rel="stylesheet" />
 ```

 At the bottom of the web page, and immediately before the `</body>` tag add a link to the `lightbox.js` file. In my case this is;

 ```html
 <script src="assets/lightbox/js/lightbox.js"></script>
 ```

(My web site is built using Jekyll, and the above lines have been added to default.html).

The script is written in javascript, and for the lightbox to work you need to ensure the jQuery JavaScript library is downloaded. You could use the one included in the lightbox2 download, but I prefer to use the edition supplied by Google via the Content Delivery Network (CDN). To implement it, add the following line to the `<head>` section of your web page at a point *before* the link to the lightbox stylesheet;

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
```

Finally, to display the pictures, add `data-lightbox="[title]"` to the picture's link. For a gallery ensure each picture in the set is assigned the same data-lightbox title. An example from my own web site is as follows;

```html

<div class="row g-1">
  <div class="col-sm-6">
    <a href="/assets/images/2020-10-27/002.jpg" data-lightbox="gallery" data-title="My First Picture"><img src="/assets/images/2020-10-27/002.jpg"></a>
  </div>

  <div class="col-sm-6">
    <a href="/assets/images/2020-10-27/003.jpg" data-lightbox="gallery" data-title="My Second Picture"><img src="/assets/images/2020-10-27/003.jpg"></a>
  </div>
</div><!--End of row-->

```

Now to test your work. Click on the pictures to see the effect. Rather professional looking, and well worth the effort!
