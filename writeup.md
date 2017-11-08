# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:
# I selected the yellow and the white lines using the HSL color space which gave me better results than the RGB space when extracting those colors.
# Then I converted the images to grayscale in order to being able to extract features from them.
# Using the grayed images, I applied the Canny algorithm to extract edges and then smoothed the images by using a Gaussian blur. This helped to reduce the noises. 
# By defining a ROI region in a form of a trapeze, I reduced the region to be considered and then applied a Hough Transformation to find lines

(Inital Image)[https://github.com/sbatururimi/Finding-Lanes-Lines/blob/master/test_images/solidYellowCurve.jpg]
[Lanes](https://github.com/sbatururimi/Finding-Lanes-Lines/blob/master/test_images_output/solidYellowCurve.jpg)

In order to draw a single line on the left and right lines, I modified the algorithm by first determining the slope of lines in order to consider separately left and right lines, then I gave a more weight to longer lines just by multiplying with the vector distance (in L2 space) between the two given points of a line. Each single line was then given by a line equation in the form of y = mx + b.

![](https://github.com/sbatururimi/Finding-Lanes-Lines/blob/master/test_videos_output/out.gif)


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the sun is much brigher and when we would have much more trees giving a much more shadows.

Another shortcoming could be to have a much more curved road.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to average the lines. Giving more weights according to the length of each segment satisified me enough but it is also possible to apply a mean to such bunch of found lines. Another improvement to this process would be  to use an interpolation technique for discrete points, like the [Least Square method](https://en.wikipedia.org/wiki/Least_squares) which would be probably more accurate that a simple mean.

We could also denoise the images by playing with different techniques like applying LUT, Non-local Means Denoising, making details sharper also. The segmentation process could improve a lot our lane finding process.