# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/canny.png
[image3]: ./test_images_output/Result.png

---
![alt text][image1]
![alt text][image3]

### Reflection

### 1. Pipeline descritpion:

The pipeline consisted of the following steps:
1) Convert image to grayscale format
2) Filter the image with Gaussian operator, this is done to allow for more smooth changes in intesity, which will allow Edge detection work better. (Canny)
3) Use Canny edge detection algorithm on the smooth image, need to fine tune the threshold parameters.
4) Create a region of interest in the canny edges image. We assume our camera is @ the center of the car and take assumptions regarding that.
5) Create line segementes using Hough Transofrm (voting of possible lines in the hough space) - need to parameterize that aswell.
   After we have line segmentes we want to connect them to coherent lines - used the assumption of having 2 lines, one left and one right, and exterpolated / averaged the line segments to left / right and continued from that.
6) Draw the lines on the original image.

The draw_lines() function was simply drawing the line segments without connecting them to full lines.
The way I connected the lines is first - segment each line segment to either 'left' or 'right' using the slope.
For all left line segments - average their intercept and slope. Using ymin/ymax of the image to find the corresponding x's. do the same for right line segments -> then draw the two lines.

### 2. Potential shortcomings of the pipeline
1) All parameter were fine tuned by hand - the edge detection and/or hough transofrm may not work aswell for images taken with different intensties etc.
2) The region of interest was also hard coded - may not generalize well enough.
3) Curved roads - exterpolating a line from the line segments may fail. (as we have a curve in that case)


### 3. Possible improvements for the pipeline

1) First improvement will be to add handling of curvy roads / line segments
2) Somehow automatically infer good parameters for Canny/Hough, perhaps fit a model while setting these as hyper parameters.
3) Figure out a dynamic good region of interest.

