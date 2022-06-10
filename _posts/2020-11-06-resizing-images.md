---
layout: post
title: Resizing Images
date: 2020-11-06
categories: photography
tags: [graphics, website, resizing, imagemagick]

---

A short guide explaining how to resize images prior to using them on a web page.

<!--more-->

I have found the best solution on a Linux/Ubuntu system is ImageMagick. This is a command line utility, but don't let that put you off. For basic resizing it is simple to use.

Check that ImageMagick is installed. If not, install it with the following command;

```
sudo apt-get install graphicsmagick-imagemagick-compat
```

Once installation is complete, you're ready to begin.

I had a batch of images, all contained within the same folder. The command I used to down size the images is detailed below, but before you try running it **bear in mind that the command will overwrite the images in that folder**. While you get to grips with this utility, I would strongly recommend you **keep copies of the original pictures in a separate folder**.

And so to the command I used, which was as follows;

```
mogrify -resize 1024 *.jpg
```
This results in the width of all the `.jpg` files being reduced to 1024px, whilst maintaining their aspect ratio.

By default the image quality is set according to the estimated quality of the original image if it can be determined, otherwise it is set at 92. If you want to set the quality yourself, this is easily achieved. The quality value must be between 1 and 100, the lower the number the lower the quality. In the next example, we set the quality level at 80.

```
mogrify -resize 1024 -quality 80  *.jpg
```

Further information concerning ImageMagick can be found at their website at [imagemagick.org](https://imagemagick.org/).
