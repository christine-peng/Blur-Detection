# Blur Detection 

Blur detection with Opencv 

There are many approaches to analyze how blurry an image is, but the best and easiest method to use is the variance of Laplacian method, which gives us a single floating point value to represent the “blurriness” of an image. This method convolves each input image with the Laplacian operator and computes the variance. If the variance falls below a predefined threshold, the image is marked as blurry. 

This method works using the Laplacian operator, which is used to measure the 2nd derivative on an image. The Laplacian highlights regions of an image containing rapid intensity changes, much like the Sobel and Scharr operators, and uses these values for edge detection. The assumption here is that if an image contains high variance, then there is a high spread of responses both along the edges and not along edges, which is indicative of a normal, in-focus image. If there is a low variance, then there is a low spread of responses, which is indicative of a blurry, out of focus images. The broad idea is the more an image is clear, the more defined edges become; the more an image is blurred, the less defined edges become.       

A challenge with this is setting the correct threshold, which can vary depending on the image. A threshold that is too low will overestimate image blur, while a threshold that is too high will underestimate image blur. 

## How it works 
1.	Install necessary packages into command prompt 
       ```
      # install opencv-python
       python -m pip install cv2
      # install imutils
       python -m pip install imutils
	```
### Modules used: 
- argparse – Used to write user-friendly command line interfaces 
        -	Arguments is used to trigger different action, specified by the action argument add_argument()
- 	imutils – Functions used to make basic image processing such as translation, rotation, resizing, skeletonization, and displaying images easier with OpenCV 
- 	opencv – Used for image and video analysis, like facial recognition and detection, license plate reading, photo editing, color filtering, edge detection, etc  

2. 	Place images in one project folder, and run command prompt to access project folder  
	```
	python blur_detection.py --images image
	```
3. 	The output will have a series of images with corresponding number, and a threshold which defines whether each image is blurry or not blurry. The default threshold is 100, but it can be changed by configuring the command prompt as such:  

		python blur-detection.py --images images --threshold 1000


