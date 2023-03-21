
Problem 1 

Crop Image

Initially, I downloaded the color image in my computer and cropped the image from the center 
out a region, the region size is half the original image as shown in the figure 1.

![image](https://user-images.githubusercontent.com/49640942/226531602-b425271f-f4b3-48f5-9324-6c625539f838.png)
Figure 1 original color image and cropped version
 
Red Channel

I demonstrated how to extract the red channel of an image and display it. The general steps for 
doing so include setting the green and blue array channels as 0. Then we can clearly get the red 
channel only. The output of this implementation shown in the figure2. For doing that I directly 
take the image array and set required channels 0. For example; img[:, :, 1] = 0 and img[:, :, 2]= 0 
which representing the blue and green channels.

![image](https://user-images.githubusercontent.com/49640942/226531651-93f653f7-4e03-4634-bb6e-946423fb03a3.png)
Figure 2 Red channel only

Gray Scale

I demonstrated how to convert an image to grayscale and display it. The general steps for doing 
so include loading the image using a suitable library such as OpenCV or PIL, converting the 
image to grayscale using cv2.cvtColor() method, and displaying it using a suitable library such as 
Matplotlib or PIL. In my sample Python code, I used OpenCV to load the image in the BGR 
format, converted it to grayscale using cv2.cvtColor() method, and displayed it using Matplotlib.
The output can be seen on the figure 3.

![image](https://user-images.githubusercontent.com/49640942/226531725-5f24e62b-7517-444c-aab2-c0e766e86545.png)
Figure 3 Gray Scale

Sobel Filter
I demonstrated how to define Sobel filters in the x and y directions, apply them to a grayscale 
image, and obtain the gradient magnitude and orientation.
The Sobel filter is a popular edge detection algorithm that uses two kernels, one for detecting 
edges in the x-direction and the other for detecting edges in the y-direction. Grayscale images 
are used for edge detection because they contain only one channel, which makes computation 
faster and simpler. The code then applies Gaussian blur to the image using OpenCV's 
GaussianBlur function to reduce noise and make the edges smoother. After applying the 
Gaussian blur, the Sobel filter is applied using OpenCV's Sobel function. Two separate filters are 
defined, one for detecting edges in the x-direction and the other for detecting edges in the ydirection as shown in the figure X. 
The Sobel filter works by convolving the image with the kernel to compute the gradient in the x 
and y directions. The gradient magnitude and direction are then calculated using NumPy's 
arctan2 and sqrt functions. 

The gradient magnitude represents the strength of the edge, while the gradient direction 
represents the orientation of the edge. The gradient magnitude is normalized to a range of 0-
255 using OpenCV's normalize function. The normalized gradient magnitude is then 
thresholded to obtain a binary edge map using OpenCV's threshold function. The threshold 
value is set to 50, which means that any pixel with a gradient magnitude less than 50 is set to 0 
(black), while any pixel with a gradient magnitude greater than or equal to 50 is set to 255 
(white).

Finally, the original image and the binary edge map are displayed using OpenCV's imshow 
function. The edge map shows the detected edges in white against a black background. 

![image](https://user-images.githubusercontent.com/49640942/226531866-3aae54ad-b1c3-4ee6-9cab-74e43215c873.png)

The Laplacian of Gaussian Filter

I applied the Laplacian of Gaussians (LoG) edge detection algorithm using the OpenCV and 
NumPy libraries. The LoG operator is used to detect edges and other discontinuities in images. 
This algorithm applies Gaussian smoothing and Laplacian edge detection in a single step. The 
output is a binary image that highlights the edges and other discontinuities in the original 
image. 

I created the function laplace_of_gaussian(), it takes a grayscale image as input along with two 
optional parameters sigma and kappa. The function applies the Laplacian of Gaussian operator 
to the grayscale image to detect edges and other discontinuities. 

The sigma parameter controls the amount of Gaussian smoothing applied to the image, and the
kappa parameter controls the threshold for detecting edges. If pad is set to True, the output is 
padded with zero border, keeping the input image size. 

I firstly applied Gaussian smoothing to the input image using the cv2.GaussianBlur() function 
from OpenCV library. If sigma is less than or equal to 0, then no smoothing is applied to the 
image. Then the Laplacian operator is applied to the smoothed image using the cv2.Laplacian() 
function. The min_map and max_map variables are computed by taking the minimum and 
maximum of the 3x3 neighborhoods of each pixel in the Laplacian image. A bool matrix is 
created for positive pixel values and negative minimum values. Another bool matrix is created 
for positive maximum values and negative pixel values. A third bool matrix is created by adding 
the previous two bool matrices. 

The resulting bool matrix represents the locations where the Laplacian of the image changes 
sign, indicating an edge. The values variable is computed by subtracting the minimum value 
from the maximum value at each pixel and scaling the result to the range 0-255. The values are 
set to 0 at the locations where the sign of the Laplacian doesn't change. If the kappa parameter 
is greater than or equal to 0, then values below the threshold are set to 0.

![image](https://user-images.githubusercontent.com/49640942/226532008-25fcadd6-b9ec-4833-b6be-a84396fac218.png)

I implemented this function on 3 different sigma values which are 1,3 and 5. As shown in the 
figure X. As we can see, if we take sigma larger, we got more smoother result. However, it 
should be noted that over-smoothing causes losing some information. Therefore, we can say 
that smaller sigma value provides finer features detected, while larger sigma value provides 
larger scale edges detected.

To sum up, I implemented the Laplacian of Gaussian (LoG) edge detection algorithm using the 
OpenCV and NumPy libraries. The function laplace_of_gaussian() takes a grayscale image as 
input along with two optional parameters sigma and kappa. The output is a binary image that 
highlights the edges and other discontinuities in the original image. The code applies Gaussian 
smoothing and Laplacian edge detection in a single step. The code is efficient and produces 
accurate results.

Problem 2

In problem 2 section a, I wrote a Python script to take live video stream from the webcam of my 
computer. I computed the gradient magnitude and the orientation on grayscale version of it
and displayed the video and the gradient magnitude on the screen. When we hit the q button, 
we can stop the recording. 

In the script, I firstly use VideoCapture function from OpenCV library to take live video scream. 
After that in a while loop I take the frame by using read() function. When I got the frames I 
converted them to gray and applied gaussianBlur function in order to get rid of noises. Then, I
created sobel arrays for x dimension and y dimension by using Sobel function from OpenCV
library. I calculated the magnitude and normalized it. I set the threshold as 25 by trying several 
values and decided 25 is the most suitable for detecting edge of me. 
I computed the fps by using OpenCV.CAP_PROP_FPS() function and put it on the scream. 

In section b, I modified the code in section a so that I can create a 15 sec video recording. I only 
put the input video and gradient magnitude by concatenating.
