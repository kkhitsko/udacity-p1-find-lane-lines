# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_gray]: ./report_images/gray.png "Grayscale"
[image_blur]: ./report_images/blur.png "Blur"
[image_edges]: ./report_images/edges.png "Edges"
[image_hough]: ./report_images/hough.png "Hough "
[image_combo]: ./report_images/combo_hough.png "Hough with image"
[image_left_side]: ./report_images/left_side.png "Left side points"
[image_right_side]: ./report_images/right_side.png "Right side points"
[image_masked_edges]: ./report_images/masked_edges.png "Masked edges"
[image_result]: ./report_images/result.png "Result image"

---

### Reflection

### 1. Pipeline description.

My pipeline consisted of several steps. 

#### Step 1. Convert image to grayscale
First, I converted the images to grayscale: 
![alt_text][image_gray]

#### Step 2. Perform Gaus blur
Then I performed gaussian blur.
![alt_text][image_blur]

#### Step 3. Canny edge
After this I used Canny edge detection algorithm to get edges:
![alt_text][image_edges]

#### Step 4. Cut region of interesting
I cutted the edges to some region of interes which supposed to be part of picture with the road we mostly interested in:

![alt_text][image_masked_edges]

### Step 5. Perform Hough transform

After this I make Hough transform to detect lines consisted of points:

![alt_text][image_hough]

![alt_text][image_combo]

#### Step 6. Separate lines by left and right side

Then I try to separate line into 2 different groups.
If points of line lies on the left side of the picture than I save it as a part of left line. Same for right line. So after this simple separation algorithm I got a tuple with 2 arrays: for left line and right line:

![alt_text][image_left_side]

![alt_text][image_right_side]

#### Step 7. Draw lane lines

Then I try to find appropriate line approximation for these points, for each side. 
Then I use `cv2.fitLine` function to get line approximation for all given point for each side. Last operation is to fit the lines in region of interest.

#### Result

![alt_text][image_result]


### 2. Shortcomings with my current pipeline


* The developed algorithm has great difficulty in determining curved lines
* Canny edge detection and Hough transform parameters are static and not changed

### 3. Suggest possible improvements to pipeline

* Make canny edges and hough transform parameters dinamically changes in different environment conditions such as weather, lightting
* Make it possible to remember the last state of the location of the lines to improve the stability of the algorithm