# **Finding Lane Lines on the Road** 

## Writeup Template


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
### 1. The Pipeline

My pipeline consisted of the following 6 steps.

1. I converted the image to grayscale.
2. defined a vertices np.array to cut out the Region of interest (roi).
3. I then applied the gaussian kernel to the ROI to remove the noise.
4. I then applied canny edge detection on the ROI (on which gaussian was already applied)
5. I then selected the hyperparameters for hough lines to apply on the resulting image.
6. After getting the hough lines, I am taking a weighted combination of the hough lines (image) and the original image, i.e. superimposing the hough lines image on the original image. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function as follows ...
1. Firstly I segregated the left side lines and right side lines by simply comparing the slopes of the lines.
2. I then took the average of the coordinates of all the detected lines.
3. I then calculated the slope (m) and b for the lines (y = mx+b)
4. I then fixed the bottom y coordinates as the size of the image and top y coordinates as some value(by trial and error) and then found out the corresponding x coordinates for right and left side.
5. I then drew single line on the left and right side of the image.

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when we encounter curves on the road i.e. we take a right turn or left turn. So we need to draw curves instead of straight lines.

Also the coordinates of the vertices for detecting the hough lines are fixed in the image so if the lines are out of bound then it is unable to detect , for that we can dynamically pass the value of the vertices to take into consideration for the processing function.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to pass the coordinates to the process function so that the algorithm can adapt with the videos having lines out of bounds of the ROI.
Another improvment would be to draw curves instead of lines for better fitting.

Another potential improvement could be to ...
