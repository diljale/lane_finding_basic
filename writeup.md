#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./examples/grayscale.png "Grayscale"

[image2]: ./examples/blurred_grayscale.png "Gaussian Blurred Grayscale"

[image3]: ./examples/edges.png "Canny Edges"

[image4]: ./examples/edges_region.png "Region of interest Mask"

[image5]: ./examples/hough_lines.png "Hough Transform"

---

### Reflection

###1. Pipeline
My pipeline consists of 6 steps. 
Step 1] Convert image to grayscale

![alt text][image1]

Step 2] Apply Guassian filter to reduce noise in the image

![alt text][image2]

Step 3] Find edges in the blurred image using Canny edge detector

![alt text][image3]

Step 4] Apply a mask to filter out edges outside our "Region of interest" defined by quadrilateral. I used image's width and height to create the mask, for example second vertex of quadrilateral is at 40% width and 60% height

![alt text][image4]

Step 5] Apply Hough Transform to detect lines in the Region of interest

![alt text][image5]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

###2. Potential shortcomings

This algorithm relies heavily on edge detection to find edge pixels and assumes that lane boundaries are on "edges" in an image. This may not work for all roads as the parameters used for edge detection may fail to detect lanes if there is not enough contrast around lane markings on the road.

The parameters used for region of interest may not work for other cameras with different resolution as lane markings may be clipped or adjacent lanes may be included as well depending on lens model in the camera.

One limitation to current approach is it can only find straight lines, in cases where road curves, lane markings will be curve and not a straight line so this algorithm will fail to detect such lane boundaries


###3. Possible improvements

A possible improvement would be to use different color space like HSV to detect edges on images where there doesn't seem enoguh contrast in RGB images. One can also build state machine which will predict location of next lane marking and use it to improve edge detection in extreme conditions where lane markings are not easily visible. 

One more improvement would be to support curved roads. This can be done by changing Hough transform to detect lines and circular curves.

Another improvement would be to make algorithm more robust by running algorithm through more data and tuning parameters