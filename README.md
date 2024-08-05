# Lane-Detection-using-OpenCV-Straight-Lanes
Overview
When we drive, we use our eyes to decide where to go. The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle. Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project, you will detect lane lines in images using Python and OpenCV. OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.

The tools we have are color selection, region of interest selection, grayscaling, Gaussian smoothing, Canny Edge Detection, and Hough Transform line detection. Our goal is to piece together a pipeline to detect the line segments in the image, then average/extrapolate them and draw them onto the image for display. Once we have a working pipeline, we will try it out on the video stream.

Lane Detection Pipeline
The lane detection pipeline consists of the following steps:

Color Selection
Region Masking
Grayscale Conversion
Gaussian Smoothing
Canny Edge Detection
Hough Transform
Draw Lines

Step 1: Color Selection.
First, let's select some colors. For instance, lane lines are usually white and we know the RGB value of white is (255, 255, 255). Here, we define a color threshold in the variables red_threshold, green_threshold, and blue_threshold and populate rgb_threshold with these values. This vector contains the minimum values for red, green, and blue (R, G, B) that we will allow in our selection.

Step 2: Region Masking.
Assuming that the front-facing camera that took the image is mounted in a fixed position on the car, the lane lines will always appear in the same general region of the image. We can take advantage of this by adding a criterion to only consider pixels for color selection in the region where we expect to find the lane lines.

We use a triangular mask to illustrate the simplest case, but we can use a quadrilateral, and in principle, we could use any polygon.

Step 3: Grayscale Conversion.
Convert the image to grayscale to reduce the complexity of the image and focus on detecting the lane lines.

Step 4: Gaussian Smoothing.
We'll include Gaussian smoothing before running Canny, which is essentially a way of suppressing noise and spurious gradients by averaging. You can choose the kernel size for Gaussian smoothing to be any odd number. A larger kernel size implies averaging, or smoothing, over a larger area.

Step 5: Canny Edge Detection.
Now, apply Canny to the gray-scaled image and the output will be another image called edges. low_threshold and high_threshold are your thresholds for edge detection.

The algorithm will first detect strong edge (strong gradient) pixels above the high_threshold, and reject pixels below the low_threshold. Next, pixels with values between the low_threshold and high_threshold will be included as long as they are connected to strong edges. The output edges are a binary image with white pixels tracing out the detected edges and black everywhere else.

Step 6: Hough Transform.
The Hough Transform is used for detecting straight lines. In Hough space, we represent the "x vs. y" line as a point in "m vs. b". The Hough Transform is just the conversion from image space to Hough space. So, the characterization of a line in image space will be a single point at the position (m, b) in Hough space.

Step 7: Draw Lines.
Finally, draw the detected lane lines on the original image. Use different colors to mark the lane lines for better visualization.

Shortcomings
Hough Transform is fit for straight lines only, in reality, curved lane lines exist where this will fail.

Solution: To handle curved lanes, more advanced techniques such as polynomial fitting for lane lines or using a sliding window approach can be applied. Libraries like OpenCV and algorithms such as the Sliding Window or Polynomial Fit are effective for detecting curved lanes.

Many roads don't have lane markings where this will fail.

Solution: In scenarios where lane markings are absent, additional contextual information such as road edges, vehicle positions, and other visual cues can be incorporated. Using machine learning models trained on various road conditions can also improve robustness in such cases.

Running the Code
To run the lane detection pipeline, use the provided Python script. Ensure you have the necessary dependencies installed and the input image or video files in place.

Dependencies
Python 3.x
OpenCV
NumPy
MoviePy
Matplotlib
Example
bash
Copy code

`python lane_detection.py`

This will process the input image or video and save the output with detected lane lines.
