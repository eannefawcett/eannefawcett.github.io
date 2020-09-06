---
layout: post
title:  "Preprocessing for Convolutional Neural Network Built with Keras"
date:   2020-08-26 21:26:13
categories: technical, data science, science
paginator: Preprocessing for Convolutional Neural Network
---

When working in data science, data is preprocessed to improve model performance. Preprocessing often includes scaling data or transforming it to create an easier to work with distribution. When working with image data this looks a little bit different than it does with numerical or categorical data.

While Keras has some great features in it's [ImageDataGenerator class][link1], there are some things that don't generalize well across entire datasets from different data sources. Some examples of this include determining the presence of alpha layers or breaking images down into their red, green, and blue components. For these particular applications, I used the library [Pillow][link2] for a [project][link3].

The first thing that I did was determine if any of the images had a preexisting alpha layer using the [".getbands()" method][link4] from Pillow's Image module. One of images I had collected did. I viewed the image without the alpha layer, and ultimately decided to discard that piece of data due to the post processing done by the original artist. The post processing had colorized and isolated aspects of the image, significantly modifying it from the original image data collected from the source fluorescence microscope in order to highlight certain features.

Next, I looked at the sizes of the original images. They were all different, shown below in Table 1.

| Width | Height |
|-------|--------|
| 1157  | 1166   |
| 1344  | 1022   |
| 1392  | 1040   |
| 1800  | 1200   |
| 1916  | 1210   |
| 1920  | 1217   |
| 1923  | 1210   |
| 1924  | 1218   |
| 2630  | 1785   |
| 2696  | 1770   |
| 2752  | 2208   |
| 2758  | 2214   |
| 3000  | 3000   |
| 3022  | 2046   |
| 3900  | 3900   |
| 4016  | 3000   |
| 4090  | 3480   |
| 4266  | 4266   |
| 4368  | 2988   |
| 4530  | 3018   |
| 4569  | 3000   |
| 4620  | 3103   |
| 4800  | 3600   |

Table 1. Widths and Heights of original image data.

After acquiring the sizes of the images, I found the smallest size for width and height and then found the average ratio between width and height. See code blocks below.

```
import numpy as np
heights = []
for image in all_images:
    heights.append(image.height)
np.array(heights).min()
```

output: 1022

```
widths = []
for image in all_images:
    widths.append(image.width)
np.array(widths).min()
```

output: 1157

```
ratios = []
for size in sizes:
    ratios.append(size[0] / size[1])
np.array(ratios).mean()
```

output: 1.3072131016891209

I used this averaged ratio in combination with the smallest width to find out what an appropriate height would be by using the code below.

```
new_height = np.array(widths).min() / np.array(ratios).mean()
new_height
```

output: 885.0890482240253

I then resized all of the images using the code below.

```
from math import floor
resized = []
for image in all_images:
    resized.append(image.resize((np.array(widths).min(), floor(new_height)), resample=1))
resized[0]
```

This code will output a resized image from the resized dataset.

The next part of preprocessing that I did using the [".split()" method][link5] from Pillow's Image module. This method splits the original images into their red, green, and blue components. This step is not necessary for preprocessing image data, but I choose to use it because I think that it will led to better performance. I am attempting to classify into two categories, present or not present. In the split images the present information stands out to the human eye; whereas, it does not in the combined RGB image.

I do plan to do additional preprocessing using Keras' ImageDataGenerator class when ready to start building the neural network. But I thought that these steps would be useful to implement before doing exploratory data analysis.

[link1]: https://keras.io/api/preprocessing/image/
[link2]: https://pillow.readthedocs.io/en/stable/
[link3]: https://github.com/eannefawcett/Fluorescence-of-Amoxicillin-Reader-Example
[link4]: https://pillow.readthedocs.io/en/stable/reference/Image.html?highlight=getbands#PIL.Image.Image.getbands
[link5]: https://pillow.readthedocs.io/en/stable/reference/Image.html?highlight=image.split()
