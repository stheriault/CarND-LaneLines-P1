# **Finding Lane Lines on the Road** 

## Writeup
### Steven Theriault

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of these steps.
1. convert image to grayscale
2. apply a gaussian blur to the grayscale image
3. mask the region of interest around the lane in front of the car
4. apply the canny transform to find the edges
5. apply a hough transform to find lines
6. filter the lines into those from the left and right lane markers
7. fit a line through the left and right lanes
8. draw the line on the image.

In order to draw a single line on the left and right lanes, I modified the
draw_lines() function by filtering the lines found in the hough transform. This
is accomplished in the filter_lines(). Lines that have an angle between 25 and
40 degs are classified as left lane markers. Lines that have an angle between
-25 and -40 are classified as right lane markers. Then, I use np.polyfit to fit
a line to the x,y cordinates of the line ends, one for the left and one for the
right lane marker. Then, in draw_lines2(), I use the fitted line to draw a line
from the bottom of the image to y=330. This give me one solid line for each of
the right and left lane markers.

You can see the jupyter notebook in the git repo

Also included in the repo are the output images and video files, so you don't
need to rerun the notebook.  But you can if you so desire.

### 2. Identify potential shortcomings with your current pipeline

potential shortcomings include:
* construction zones where there are no lane markers, there would be nothing to
find
* curves in the road, I'm fitting a line to the line segments, so a curve would
defeat my approach

### 3. Suggest possible improvements to your pipeline

possible improvements include:
* use a quadratic curve to fit to the lines segments from the hough transform
to match curves in the road
* track the movement of the lanes, frame to frame, to filter the jitters in the
lane tracking.
* track other items in the video to help improve the spatial awareness of the
processor
