# **Finding Lane Lines on the Road - Image Thresholding** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

[//]: # (Image References)

[image1]: ./test_images/signs_vehicles_xygrad.png "Reference"
[image2]: ./images/sobel-combination.png "Sobel"
[image3]: ./images/color_channels.png "Color channels"
[image4]: ./images/filters2.png "Color filters"
[image5]: ./images/stacked.png "Stacked filters"

In this small project we are calculating the [Sobel gradient](https://en.wikipedia.org/wiki/Sobel_operator) of an image and apply different thresholds in order to optimise the detection of lane markings. Additionally, we are looking at different color spaces to find a better way to distinguish white and yellow lane markings.

A combination of normal gradient thresholds and directional thresholds yields a clear highlighting of lane markings:


| ![Reference][image1] | ![Sobel Thresholding][image2] | 
|:--:|:--:| 
| *Reference image* | *Sobel Thresholding* |

 So far, we have restricted ourselves to grayscale images converted from RGB only. However, to make better use of the color information in our images it makes sense to examine other color spaces as well. To this end we will examine our image in HLS and HSV color space:

 ![Color spaces][image3]

 As we can see, it seems like the S-channels alone do a very good job of filtering for the yellow line in this image. If we restrict ourselves to RGB then the R-channel seems to do the best job.Let's have a look at the more complicated filter I used in project 1 and compare it to a direct threshold filter on the HLS S channel combined with the R channel.

 ![Color filters][image4]

It seems like the more sophisticated filter from Project 1 coincidentally still performs better but it might still be worth to test both filters under different lighting conditions.

In the end we create a pipeline which combines Sobel gradients with color filters to create a stacked image, in order to see the contribution of each method:

 ![Stacked filters][image5]