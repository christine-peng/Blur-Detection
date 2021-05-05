# Blur Detection 

Blur detection with Opencv 

There are several approaches to analyze how blurry an image is using the Computer Vision Python package, with the most noteworthy methods being the Laplacian transformation, the Sobel filter, the Canny Edge detector, and the Fast Fourier Transform. 

The Laplacian transformation, while not being the perfect solution, is the easiest method to distinguished between focued and blurred images. It operates by outputting a single floating point value to represent the “blurriness” of an image. This method convolves each input image with the Laplacian operator and computes the variance. If the variance falls below a predefined threshold, the image is marked as blurry. 
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
2.      Run the program, which: 
	- Loads an image
	- Converts the original image to grayscale
	- Applies a Laplacian operator to the grayscale image and stores the output image
	- Displays all ".jpg" files in file path, with a pre-defined threshold which determines whether the image is "blurry", or "not blurry".  

3. 	Place images in one project folder, and run command prompt to access project folder  
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


Contrary to what I had initially thought, the Laplacian method seems to work well for images with reflections. 
![image](https://user-images.githubusercontent.com/83466109/117076774-d40f5a00-aceb-11eb-829f-8263a25ea2c7.png)
The method also seems to work well for images with an object of interest and a blurred background, although the values given were substantially lower compared to other images without a blurred background. 
![image](https://user-images.githubusercontent.com/83466109/117078580-fd7db500-acee-11eb-9f43-eead8035bd86.png)

### Limitations: 
There are several limitations to using the Laplacian method to detect blur. The method requires manual tuning to define the threshold which determines whether an image is blurry. Perception of image sharpness is based on edges, not the histogram or other spread-functions. It does not reflect other factors present in imagery such as motion blur, shaking, positioning errors, changing lighting positions, environmental factors, etc. If lighting conditions, environment, and image capturing process are not well controlled, there would be mixed results. For example, the image with snow was mis-defined as "blurry" because snow shows subtle changes in edges in spite of clarity in image quality.  
![image](https://user-images.githubusercontent.com/83466109/116952409-73c2de80-ac3f-11eb-99c3-5a8722971a62.png)

I thought partial motion blur in images could be a potential problem; however, based off the images I used, this method seems to have no problems distinguishing motion blur from overall image clarity. The values for given images below were all correctly identified as "not blurry". Given this result, there could be potential partial blurs in drone imagery as result of rain droplets or motion that may be misinterpreted as "not blurry" when in actuality it is partially blurry. Testing drone imagery with partial bluring may be necessary to get a better sense of how effective this approach is for drone-specific images.  

![image](https://user-images.githubusercontent.com/83466109/117081148-2a809680-acf4-11eb-989f-558e7e45302f.png)

