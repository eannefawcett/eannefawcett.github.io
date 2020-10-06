---
layout: post
title:  "Letting Your File Names Work for You: Using Python's Pillow Library to Iterate Over File of Images"
date:   2020-09-29 21:26:13
categories: technical, data science
paginator: Letting Your File Names Work for You
---

Lately I've found myself needing to open many images at a time to work on a data science project. So, I thought I would share a method to do this without using "hard code", or using each file name independently, in order to make my code more pythonic.

Depending on how you name you files, you can iterate over them. Using a base string like 'image', then following that up with a number, and finally and ending, like '.jpg' allows you to iterate over the files. If you have let's say twenty-eight images to open, then you can use the following code to store your images in a list so that you can work with them using iteration or looping.

```
import PIL import Image
path = '../images/'
base = 'image_'
ending = '.jpg'
images = []
for image in range(0, 28):
  images.append(Image.open(path+base+str(image)+ending))
  ```

This 'path + base + iterator + ending' structure can also work with other python libraries like os and json. The '../' part of the path variable takes you back to your root directory in case you want to access things that are stored in a different file but in the same root directory. And if you have different endings you can use a try/except or an if/elif/else statement with the different endings changing. Also, if your base changes from images to something like red, green, blue because you separated out your images, you can use a nested for loop structure to get at all of the files.
