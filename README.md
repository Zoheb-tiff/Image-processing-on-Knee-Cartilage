# Image-processing-on-Knee-Cartilage
Knee cartilage segmentation by thresholding and morphological operation; Finding area and maximum thickness of cartilage; Finding boundary of cartilage

1.	Segment cartilage using thresholding and or morphological operations.

Here we read the dicom file and display it.
The data type is converted from uint16 to double for normalization, else all decimal data will be lost and only 0s and 1s will be preserved.
To avoid dealing with the unrequired portion and complicating the algorithm further, we first segnment the portion we are concerned with. This can be done by two ways. Use of function imcrop(img) or manually assigning the portion unrequired with the value 0. The latter one serves the image size.
To segnment using thresholding, as we need to have a band of intensities preserved which we make out using the data tip, we write a loop to segnment it out and assign it as value 1, and the rest 0.
To remove unwanted speckles, we use the function imerode(img,strel) with a square structuring element.

2.	Find area of the cartilage (assume pixel size = 0.5 by 0.5 mm)


We have a binarized image, hence we can convert the data type back to uint16. Then we find total number of elements with the value 1, and multiply it with the area of one pixel. This gives us the area of the segmented section.

3.	Find maximum thickness of cartilage

We create a vector with length = one of the dimensions of the normalized image. We then convolve it with the normalized image and take only that element which has overlapped with the normalized image fully and slides across the width. We then find the maximum element of the array which we obtain after multiplying the vector to the normalized image, and multiply the thickness of a pixel (0.5 mm) with the sum of the maximum element.

4.	Find the boundary of the cartilage using Gradient, Laplacian and morphological operations and compare results.

Gaussian edge detection method is first derivative of the intensity in the direction mentioned. First derivative can be found by ways like Sobel, Prewitt, Robert’s. The differentiating factor being the window being multiplied to the image.
Laplacian edge detection method is the second derivative of the intensity. Double edges are detected and then zero crossing is found. Smoothening is done first and then laplacian of it.
Morphological edge detection is done by subtraction of the result of dilation and erosion.

