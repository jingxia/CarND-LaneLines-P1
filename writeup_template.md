
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 10 steps. 

1. Convert the image to HSV. This makes creating masks for different colors easier.
2. Create a mask for the white pixels and a mask for the yellow pixels.
3. Create a combined mask by taking the bitwise OR for the white and yellow masks.
4. Apply the color mask to the original input image.
5. Convert the masked image to grayscale.
6. Apply a Gaussian blur.
7. Apply a region mask in the shape of a trapezoid.
8. Apply Canny Edge Detection.
9. Draw interpolated and extrapolated lane lines after running the image through Hough Lines. More on this below.
10. Combine the final lane lines with the original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by adding the following processing steps:

Take the lines parameter, which is a collection of line segments, and separate it into two buckets: Left Lines and Right Lines. This is determined by calculating the line segment's slope. Lines with a positive slope are put into the Left Lines bucket, and otherwise they are put into the Right Lines bucket. 

For each bucket of line segments, I calculate the average location of the top and bottom of the right and left buckets when the line segments are extrapolated out.

For movies only: If drawing lanes for a movie, then I use the moving average of left and right lanes based on the last several movie frames. 



### 2. Identify potential shortcomings with your current pipeline

One of the problem is that the result is not perfectly robust. When there is a white or yellow car close to the line, it confuses with that and makes the line shift. 

Another problem is that it cannot handle turns. 

Also it cannot handle lane shifting. 


### 3. Suggest possible improvements to your pipeline

When doing the line average, add a filter and only keeps the lines that are close enough and the most close to the center of the picture, so that it only keeps the most centered lines if there are multiple lanes. This should make the lane detaction more stable. 

Also determine other objects like cars, so that there's less confusion with lanes. 

