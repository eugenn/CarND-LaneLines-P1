#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

My pipeline consisted of 5 steps.
* Convert the images to grayscale
* Perform Gausian smoothing and apply Canny edge detection
* Select region of interest and mask other areas of the image
* Apply Hough Transform to detect lane lines
* Extrapolate parts of lines retrieved from the first step to one long line 
  and to map on the original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by the following way.
The main idea is to find point of intersection with axis X using two points belongs to source lines and it slope value.
As we know the equation of a line is Y = m*X + b, where m - slope, b - Y-Intercept, then
b = Y - m*X, X = (Y - b) / m
In order calculate these params, I find average values of slope and Y, after that Y-Intercept and 
location where line interest X axis - X point.

If you'd like to include images to show how the pipeline works, here is how to include an image: 


[image2]: ./test_images/solidWhiteCurve_after.jpg
[image3]: ./test_images/solidWhiteRight_after.jpg
[image4]: ./test_images/solidYellowCurve_after.jpg
[image5]: ./test_images/solidYellowCurve2_after.jpg
[image6]: ./test_images/solidYellowLeft_after.jpg
[image7]: ./test_images/whiteCarLaneSwitch_after.jpg

![image2]
![image3]
![image4]
![image5]
![image6]
![image7]

**2. Identify potential shortcomings with your current pipeline**


Potential shortcomings of my approach:

* Not well works in case when road more curved
* The region of interest in Image masking is static and in some cases it failed 


**3. Suggest possible improvements to your pipeline**

A possible improvement would be to 
* Use dynamic masking
* Use more smart approach for excluding lines with to high deviation from expected position