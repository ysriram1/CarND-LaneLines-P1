# **Finding Lane Lines on the Road**

#### In this project, we built a simple pipeline that is able to process road images taken by a car camera and detect lanes. The pipeline function is then used to run through two different videos to continuously detect lanes.

---

### Goals

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Use the pipeline function to continuously find lanes in road video


[//]: #

[image_A]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/masked.png "masked"

[image_B]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/gray.png "grayscale"

[image_C]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/gaussian.png "gaussian"

[image_D]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/edge.png "edge"

[image_E]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/hough.jpg "lanes"

[O1]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidWhiteCurve.jpg
[C1]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidWhiteCurve.jpg

[O2]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidWhiteRight.jpg
[C2]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidWhiteRight.jpg

[O3]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowCurve.jpg
[C3]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowCurve.jpg

[O4]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowCurve2.jpg
[C4]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowCurve2.jpg

[O5]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowLeft.jpg
[C5]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowLeft.jpg

[O6]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/whiteCarLaneSwitch.jpg
[C6]: https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/whiteCarLaneSwitch.jpg


---

### Reflection

### 1. The Pipeline

Our pipeline consisted of 5 main steps:
- First the the parameters of a polygon mask to apply to the image are determined [A]. These parameters are chosen in such a way that none of the actual lanes are masked in all images generated by a camera held in the same position. However, the mask not applied yet, it applied later once we detect the necessary lines.

- Then, the image is transformed from color to grayscale [B].

- Next, a gaussian blurring is applied to the image to remove noise [C].

- A canny edge detector is applied to the blurred image to detect edges [D]. Since the image is blurred, the noise in the original image is unlikely to be detected by the canny detector.

- Once, the edge image is generated, hough transformation function is applied to find lines in the image. The hough transformation is applied by using a custom draw_lines() function. This function is modified in order to elongate the lines of the two lanes through a process of calculating an average right lane and left lane based on the slopes of the lines, elongating the lines based on the slope and the coordinates of the mask, and applying the polygon mask to only use lines with-in the mask area to prevent any non-lane lines from interfering [E].

It is worth mentioning that the determination of the mask coordinates, the application of gaussian blurring, edge detection, and the hough transformation process involved a significant amount of parameter tuning in order to detect lines that at least approximately represented the actual lanes in the image.

<ul>
<strong> A </strong>
<img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/masked.png"> <br>
<strong> B </strong>
<img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/gray.png"> <br>
<strong> C </strong>
<img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/gaussian.png"> <br>
<strong> D </strong>
<img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/edge.png"> <br>
<strong> E </strong>
<img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/pipeline_results/hough.jpg" style="width:40%"> <br>
</ul>

### 2. Testing

The pipeline described in the previous section has been applied to different test images. The following results were obtained:

<table style="width:100%">
<tr>
<td> <strong> Original </strong> </td>
<td> <strong> Lanes Detected </strong> </td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidWhiteCurve.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidWhiteCurve.jpg">
</td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidWhiteRight.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidWhiteRight.jpg">
</td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowCurve.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowCurve.jpg">
</td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowCurve2.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowCurve2.jpg">
</td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/solidYellowLeft.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/solidYellowLeft.jpg">
</td>
</tr>

<tr>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images/whiteCarLaneSwitch.jpg"> </td>
<td> <img src="https://github.com/ysriram1/CarND-LaneLines-P1/blob/master/test_images_output/whiteCarLaneSwitch.jpg">
</td>
</tr>

</table>



### 3. Identify potential shortcomings with your current pipeline

Based on the results obtained by running our algorithm on the test images and on the test videos, we notice that the performance is acceptable, but there is scope of improvement. Here are some shortcomings:

- Applying the polygon mask after identifying the lanes results in lane lines being cut-off if the slopes and positions of the elongated lane lines are not near the actual lanes.

- Did not properly eliminate extreme slope values when elongating the lines.

- Code is verbose and contains redundancies.

- The current pipeline is only applicable to images taken by the same camera in the same orientation.


### 4. Suggest possible improvements to your pipeline

Some potential improvements:

- Auto decide the parameters based on the image and mask rather than using previously decided global parameters.

- Remove extreme slope values prior to elongating the lines.
