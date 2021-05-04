# Blur Detection 

Blur detection with Opencv 

There are many approaches to analyze how blurry an image is, but the best and easiest method to use is the variance of Laplacian method, which gives us a single floating point value to represent the “blurriness” of an image. This method convolves each input image with the Laplacian operator and computes the variance. If the variance falls below a predefined threshold, the image is marked as blurry. 
			<p align="center">
			![image](https://user-images.githubusercontent.com/83466109/117067306-b1c30f80-acde-11eb-8959-174554b5a57a.png)
			</p>
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
2. 	Place images in one project folder, and run command prompt to access project folder  
	```
	python blur_laplacian.py imagepath
	```
### Modules used: 
- argparse – Used to write user-friendly command line interfaces 
        -	Arguments is used to trigger different action, specified by the action argument add_argument()
- 	imutils – Used to make basic image processing such as translation, rotation, resizing, skeletonization, and displaying images easier with OpenCV 
- 	opencv – Used for image and video analysis, like facial recognition and detection, license plate reading, photo editing, color filtering, edge detection, etc  

## Results Analysis 
The results show a list of images with corresponding description detailing whether each image is blurry or not blurry, followed by the focus measure. A pre-defined threshold is used to determine what value can be marked as blurry. Any number that falls below the threshold will be marked as "blurry", and any number that falls above the threshold will be marked as "not blurry". A value of 100 seems to work for my dataset, but this number is subject to change according to the content of the images. Below shows each image on the left side, with their corresponding blur level output on the right side. Image4 was unfortunately unable to give me a value, this could perhaps be due to the fact that this image was named with a capital "JPG", whereas the script specified to only output images with the lower case "jpg". I was unable to change the capitalization of this image item type because I don't have permission to do so. I added three more images in addition drone imagery from FYBR to further comprehend how well this tool works.  

![image](https://user-images.githubusercontent.com/83466109/116951153-02356100-ac3c-11eb-851a-710127da53c0.png)




### Limitations: 
There are several limitations to using the Laplacian method to detect blur. The method requires manual tuning to define the threshold which determines whether an image is blurry. This method only works well if lighting conditions, environment, and image capturing process are well controlled; otherwise, there would be mixed results. For example, the image with snow was mis-defined as "blurry" because snow shows subtle changes in edges in spite of clarity in image quality.  
![image](https://user-images.githubusercontent.com/83466109/116952409-73c2de80-ac3f-11eb-99c3-5a8722971a62.png)

Partial motion blur in images is also not reflected well using this method. The image below is mostly clear with some motion blur, yet the output shows a value that is quite high, indicating the image is "not blurry". This may be problematic as partial motion blur may be common in drone imagery, yet the image may be mis-interpreted as clear when it is actually partially blurry.  
![image](https://user-images.githubusercontent.com/83466109/116952840-8b4e9700-ac40-11eb-9d63-b7b4d32712f7.png)
