# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./writeup_images/road_with_dip.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of the following 6 steps:
1. First, I converted the images to grayscale
2. Prepared the images for the next step by running a Gaussian blur filter on them with a kernel size of 5
3. Ran canny edge detection on the images
4. Filtered the image from the previous step to only a region of interest, which would include the area around the lanes only.
5. Ran a hough transform to detect lines in the image. 
6. Draw an aggregate of the detected lines as the lanes on the original image. 

To improve the draw_lines() function, I first separated all the detected lines into two sets, one with all the lines with a positive gradient, and the other with all the lines with a negative gradient. I then took an average of the gradients and intercepts in the two sets, filtering out the outliers, to then draw the two lines as the left and right lanes on the image. 


### 2. Identify potential shortcomings with your current pipeline

My pipeline works well with relatively straight lines and a flat road, but starts to fall short when the road curves or when the road isn't 'flat' as is the case in the following image: 

![road with dip][image2]

This is because I have hard-coded the top of the straight lines on the y-axis, to a point that works generally well for the images we worked with. 

### 3. Suggest possible improvements to your pipeline

A possible improvement could be to use variable lengths for detected lines drawn on the output image so that the two lines together capture the sense of 'curvature' and 'slope' of the road. 

E.g., if the road curves left, the left line would be shorter than the right line, and vice versa. Similarly, if the road dips, then both the lines would be shorter than they would be otherwise. 

Another possible improvement is to not force the lines to be flat lines but rather let them be curved lines as well. We could use linear regression to fit a curved line to the several detected lines, which are just a collection of points. 
