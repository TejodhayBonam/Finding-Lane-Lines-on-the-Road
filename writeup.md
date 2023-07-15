# **Finding Lane Lines on the Road** 

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

My pipeline consisted of 7 steps. 


1. First, I converted the images to grayscale
2. then I blurred the gray image using guassian blur.
3. Using Canny I produced an image with white edges and everthing else in black
4. Then I kept the edges within the interested region, wiping everthing else out by turning them to balck.
5. Using Hough lines transformation I found lines in the region and drew them in red.
6. I synthesised a new image from the original image and the image from step 5. In the new image lane lines are in red.
7. I printed and saved the new image to disc.

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by the following steps.
1. Found out the longest line among all lines, calculated its slope.
2. Based on the slope from step 1, classified all lines to two groups, indicating left and right lines
3. Calculated the slope by finding the longest line from the other group.
4. Found the top point and bottom point for both sides using the equation y = m * x + b
5. Top point and bottom point formed the long solid line for each side. Drew the line. 

I also tried using the averaging the slopes of all lines for both sides instead of using the slope for the longest lines. Didn't work well. I guess I need to give different lines different weights while averaging them. But based on what metrics? I can also exclude outliers who contribute noise to the averaging. Might be the better way.

You cam look up the output images in P1.ipynb.


### 2. Identify potential shortcomings with your current pipeline

In the video proudced by using my customized `draw_lines()`, the two lines are trembling. Wonder what improvement can be made to make them steady. It could be the outliers in the lines causing this.

I introduced some bugs when implementing `draw_lines()`. I thought about testing afterwards. I should extract the steps to seperate methods. Unit test them. Stub method calls and use dummy data to test them in isolation. I would've done that if I were familiar with ipython testing or python testing and had the time. I could use some good suggestions here.


### 3. Suggest possible improvements to your pipeline

Improvements can be made upon the shortcomings above.

Besides, my implementation can not handle the challenge video. From the slack channel I noticed it's about excluding outliers. From the video we can see that the right lane line is more curved than lines in other videos. This means outliers. There are several algorithms available. I'm kind of behind the schedule so I decide not to implement them here.