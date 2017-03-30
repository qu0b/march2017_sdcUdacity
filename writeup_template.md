#**Finding Lane Lines on the Road**

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_images_output/cannyTransform.jpg "cannyTransform"
[image3]: ./test_images_output/guassianBlur.jpg "guassianBlur"
[image4]: ./test_images_output/polyTransform.jpg "polyTransform"
[image5]: ./test_images_output/houghLineTransform1.jpg "houghLineTransform1"
[image6]: ./test_images_output/houghLineTransform.jpg "houghLineTransform1"
[image7]: ./test_images_output/weightedTransform.jpg "weightedTransform"
[image8]: ./test_images_output/weightedTransform1.jpg "weightedTransform1"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale

![alt text][image1]

then I applied the canny transformation
![alt text][image2]
choosing a 1:2 ratio with the lower threshold being 200 and the higher threshold being 400. From what i recall anything under 200 is dropped 200 to 400 will be included if connected to strong edges 400 is transformed. Next I applied the Gussian Blur after the Canny transformation, giving me a nice blur over the edges.
![alt text][image3]
Next, I defined the polynomial to lay over the image.
![alt text][image4]
This took a while as the inverse y coordinates are very confusing at first. After finally finding reasonable values I applied the hough line transformation. The variables chosen are mainly due to trial and error with no specific reasoning. Long connected lines are what I was looking for in general.
![alt text][image5]
After finishing up I combined the hough line transform with the original image and gave that as an output to my function.
![alt text][image8]
In the end I had a function that did all the 5 steps sequentially returning the transformed image in the end.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by this part was tricky. In the end I had to find the equation for each line and find the coordinates of the top and of the bottom relative to the pictures' coordinates. To get better results I limited the top to the top of my polynomial.

![alt text][image7]



###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when well obviously a shortcoming is the mathematical standpoint, I did not include any error handling. Cases such as having a white car, missing line lanes for a longer period and sharp turns could be problematic. Further, it would be necessary to ensure that the draw_lines() function does not divide by zero or that the float value is not infinite.

Another shortcoming could be that the pipe does not consider anything other than straight lines.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to error handling especially in the draw_lines function.

Another potential improvement could be to store previous lines in order to reduce variance for future lines.
