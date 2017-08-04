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

### 1. Pipeline description.

My pipeline, coded in the "draw_lines_pipeline" consist of 8 steps:
1. The original image is converted to grayscale.
2. The grayscale image is smoothed with Guassian Smoothing to remove lesser edges.
3. Canny edge-detection algorithm is applied to the blurred image.
4. The area os interest for the next step is limited to  only the portion of the image showing the road in front, all the rst is blackened.
5. Straight lines are detected using Hough Transform. The output of this stage is a number of lines described by their endpoints.
6. All the detected lines are sorted into bins along with other similar lines. Similarity is assessd by comparing and updating m (actually, angle, to have a linear quantity) and b coefficients. There's no predefined limit to the number of bins, so in principle no limit to the number of lines/lanes the pipeline can detect (i.e. only left and right).
7. For each of these bins, an "average line" is computed.
8. The lines obtained are drawn as an overlay on the original image.


### 2. Potential shortcomings with my current pipeline

* If the region of interested is expanded, it's easy to detect the side of the road as a line. This can actually be positive, but then there's a need to define it as "edge of the road" and not as a line.
* The line drawing funciton cannot deal with horizontal lines. It can be obviously improved.


### 3. Possible improvements to my pipeline

* There no reason to process the whole image (i.e. grayscaling, applying gaussian smoothing or Canny), if only the region of interest is then considered. This could speed up the code.
* Probably a more efficient sorting algorithm can be used to sort all the lines detected by the Hough transform into bins.
* Not treating each frame of the video separately but using previous knowledge (i.e. the location of the lines in the previous N frames, for example by averaging) can result in smoother line detection and reduce flickering.
