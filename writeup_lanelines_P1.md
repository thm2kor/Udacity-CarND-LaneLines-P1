# **Finding Lane Lines on the Road** 


---

## Objective**

The objective of this project is to build a pipeline that finds lane lines on the road. In addition, i would use this report to reflect on the key lessons from my work.

---

## Reflection

### 1. Description of the pipeline
The pipeline is developed around the helper/wrapper functions provided by Udacity as a part of the workspace. The pipeline steps would be illustrated with the following image:
[image1]: ./examples/solidWhiteRight.jpg "Reference"

My pipeline consisted of the following sequential steps:
1. First, the input images are converted to grayscale
[image2: ./examples/grayscale.jpg "Grayscale"

2. Next, a gaussian blurring is applied to reduce some spurious edges, thereby reducing the amount of noise present in the image. 
[image3: ./examples/gaussian_blur.jpg "Gaussian Blur"

3. After this, the Canny transform is applied to get the gradient edges. The thresholds for the gradients and the kernel size were anchored on the values which was discussed in the course. The traffic scenario and the color scheme looked very similar to the image discussed in the course
[image4: ./examples/edges.jpg "Edges"

4. A trapeziodal region at the lower center of the image was defined to mask out the lanes. By analysing (trial and error method) the given images and videos, a lit of padding was added and removed to the trapezoid to get the best possible region of interest.
[image5: ./examples/masked_edges.jpg "Masked Edges"

5. A Hough transform is applied on the masked edges. The parameters were determined based on the trial and error method. The length of longer lane segments in the images were used as an anhoring point to decide the min_line_length and max_line_gap
[image6: ./examples/lines.jpg "Line segments"

6. The resulting straight lines from the Hough transform are blended into the source image to derive the target image.
[image7: ./examples/edges_result.jpg "Final"

7. In the next improvement step, the segements highlighted in the left lane and right lane are drawn as single line in the draw_lines_extended function. 
- The end points (x1, y1, x2, y2) of each line segments from the hough tranform are consolidated in separate arrays. Based on the direction of the slope, the points are clustered in seperate arrays. 
- Using the cv2.polyfit, the slope and y-intercept for the left lane and right lane are derived
- A straight line is drawn from the left bottom to the top left point (which is modelled from the slope and the y-intercept derived from the previous step
- A similar line is drawn for the right lane.
- A sample output from the above function:

---
### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...
Trial error method
Straing line fit
Another potential improvement could be to ...
