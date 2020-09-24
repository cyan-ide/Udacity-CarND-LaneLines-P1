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

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consisted of 5 steps, similar as class examples during the lessons;
* 1. Convert to grayscale
* 2. Remove noise (Gaussian smoothing)
* 3. Detect line edges (using Canny alg)
* 4. Mask the unwanted portions of image (ie. the area that does not contain lanes is turned black, mask coords hardcoded)
* 5. Turn detected edges (pixels) into lines (coordicantes of start and end line) (using Hough transform)

First appraoch \[testing on still images] (unmodified draw_lines - in submitted code called draw_lines_org ):
* I used same/similar parameter settings as with the lesson code samples, jsut modifed the hardcoded coordinates of the mask

Second appraoch (**modyfing draw_lines** to have only one line per left lane marking and one for right):
* calculate (a) slope and (b) intercept parameters for each line detected with Hough transform (ie. y = ax +b )
* distinguish between left and right lane marking based on slope value (ie. different angles will result in negative or positive slope)
* record seperatly slope/intercept for lines that belong to left / right markings and at the end average them out to come up with a single line per each left/right

Third approach (**forther modyfing draw_lines**)
* add additional condition to remove horizontal lines, in two first videos those would show up sometimes as bottom edges of the dotted lane markings. When applying average that would cause the final line slope to have a big error vs real lane mark.


If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
