# finding-lane-lines-project
Finding Lane Lines on the Road

•	Software/Tool Used: Google Colaboratory.

•	Overview:
 	This project defines a method to detect Lane lines in a road in order to safely guide and maintain the car on a specific lane. The goal is to detect the white lines.
 	
•	Lane Detection Pipeline: 
1.	Convert original image to grayscale.
2.	Darkened the grayscale image (this help in reducing contrast from discolored regions of road)
3.	Apply slight Gaussian Blur.
4.	Apply canny Edge Detector (adjust the thresholds — trial and error) to get edges.
5.	Define Region of Interest. This helps in weeding out unwanted edges detected by canny edge detector.
6.	Retrieve Hough lines.
7.	Consolidate and extrapolate the Hough lines and draw them on original image.

I.	Convert to grayscale:
Converting original image to grayscale has its benefit. We have to find yellow and white lanes, and converting original image to grayscale increases the contrast of lanes with respect to road.

II.	Darken the grayscale image:
This is done with the intent of reducing contrast of discolored patches of the road.

III.	Gaussian Blur:
Gaussian blur (Gaussian smoothing) is pre-processing step used to reduce the noise from image ( or to smooth the image). We use this pre-processing step to remove many detected edges and only keep the most prominent edges from the image.

IV.	Canny edge detection:
we apply Canny edge detection to these Gaussian blurred images. Canny Edge Detection is algorithm that detects edges based on gradient change. Not that the first step of Canny Edge detection is image smoothing with default kernel size 5, we still apply explicit Gaussian blur in previous step. The other steps in Canny Edge detection include:
•	Finding Intensity Gradient of the Image
•	Non-maximum Suppression
•	Hysteresis Thresholding

V.	Select region of interest:
Even after applying Canny Edge Detection, there are still many edges that are detected which are not lanes. Region of Interest is a polygon that defines area in the image, from where edges we are interested. Note that, the co-ordinate origin in the image is top-left corner of image. Rows co-ordinates increase top-down and column co-ordinates increase left-right.
VI.	Hough Transformation Line Detections:
Hough Transform is the technique to find out lines by identifying all points on the line. This is done by representing a line as point. And points are represented as lines/sinusoidal(depending on Cartesian / Polar co-ordinate system). If multiple lines/sinusoidal pass through the point, we can deduce that these points lie on the same line.
VII.	Consolidation and extrapolation of the Hough lines
We need to trace complete lane markings. For this the first thing we need to distinguish between left lane and right lane. There is easy way of identifying left lane and right lane.
•	Left Lane: As the values of column co-ordinate increases, the values of rows co-ordinate decreases. So the gradient must be negative.
•	Right Lane: As the values of column co-ordinate increases, the values of rows co-ordinate increases. So the gradient must be positive.
•	We’ll ignore the vertical lines.
After identifying left lane and right lane Hough lines, we’ll extrapolate these lines. There are 2 things we do:
1.	There are many lines detected for Lane, we’ll average the lines
2.	There are some partially detected lines, we’ll extrapolate them.

•	Conclusion:
In this project, we implemented a lane detection preprocessing and ROI(Region Of Interest) selection methods to design a lane detection system. The main idea is to add white extraction before the conventional basic preprocessing. Edge extraction has also been added during the preprocessing stage to improve lane detection accuracy. We also placed the ROI selection after the preprocessing. Compared with selecting the ROI in the original image, it reduced the nonlane parameters and improved the accuracy of lane detection. Currently, we only use the Hough transform to detect straight lane.
