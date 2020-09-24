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

**First appraoch** \[**testing:** Still images] (unmodified draw_lines - in submitted code called draw_lines_org ):
* I used same/similar parameter settings as with the lesson code samples, jsut modifed the hardcoded coordinates of the mask

**Second appraoch** \[**testing:** Still images] (**modyfing draw_lines** to have only one line per left lane marking and one for right):
* calculate (a) slope and (b) intercept parameters for each line detected with Hough transform (ie. y = ax +b )
* distinguish between left and right lane marking based on slope value (ie. different angles will result in negative or positive slope)
* record seperatly slope/intercept for lines that belong to left / right markings and at the end average them out to come up with a single line per each left/right

**Third approach** \[**testing:** First two videos] (**further modyfing draw_lines**)
* add additional condition to remove horizontal lines. In two first videos, with my Canny/Hough paramters, horizontal lines would show up sometimes as bottom edges of the dotted lane markings. When applying average that would cause the final line slope to have a big error vs real lane mark. This showed a problem/importance of line length parameter of Hough transform:
  * If too short the horizontal lines of the dotted lane lines are detected (and cause a problem when averaging the lane lines)
  * If too long the vertical lines of the dotted lane lines are not detected (or less of them are detected, e.g. the short ones on the horizon are missed out; if lines on the horizon are not detected before the the line on the bottom of screen disappears then there is no line detected at all)

**Fourth (final) appraoch** \[**testing:** challange video] (**further modyfing draw_lines and parameters **)
* the challnage video comes in different resolution, therefore before doing any processing I rescale it to first two videos size (as my mask parameters were hardcoded rather than percent values)
* in the challange video the core problem seems to be changes in light intensity. With the initial Canny paramters some lines wouldn't get detected at all (in bright light) or too many would in high contrast areas
* (1) first modification was too greatly lower the threshold of Canny algorithm (that resulted in big amount of 'noise')
* (2) second modification was to filter out unwated lines, those turned to be mainly horizontal, so I further increased the condition on slope (ie. for two initial video I was about 0.3, for the final video to work I had to further constrain to 0.55)
* (3) some checks for exceptions like no lines detected at all. Ddue to all constraints the detected lines are typically where one woudl expect, however sometimes no lines are detected at all, I considered that 'better' than having the angle of deteced line completly off.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
