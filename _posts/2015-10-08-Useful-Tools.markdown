---
layout:     post
title:      "Useful Tools"
subtitle:   "Some useful tools"
date:       2015-10-08 12:00:00
author:     "Shi"
---



# Automatic build and deploy tool

[Fastlane](https://fastlane.tools/)



# Image

## ImageMagick

### Resize Image

convert tutorial_1.png -resize 768x1280 tutorial_1.png 

### Reduce image dimention

convert tutorial_1.png -colors 255 tutorial_1.png 

### specify a compression level for JPEG images

convert howtogeek.png -quality 95 howtogeek.jpg

### Resize an image to a width of 200 while preserving the aspect ratio

convert example.png -resize 200 example.png

### Resize an image to a height of 100 while preserving the aspect ratio

convert example.png -resize x100 example.png

### Rotating an Image

convert example.png -rotate 90 example.png

### Batch modify images

mogrify -path fullpathto/temp2 -resize 60x60% -quality 60 -format jpg *.png

mogrify -format jpg *.png



##SSL

[Free, open source SSL](https://letsencrypt.org/) 


