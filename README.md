#**Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

_The goals of this project_

*   Finding two line models for left and right lanes on the road based on camera images



_The steps of this project are the following:_

*   ROI masking

*   Edge detection
    *   Gray scaling
    *   Gray scale reinforcement of lane color region
    *   Gaussian filtering
    *   Canny edge detection
* Line estimation
  - Hough transform
  - Line segment
  - False filtering
  - RANSAC algorithm


---

### Reflection

###1. Pipeline for lane detection

​	My pipeline consisted of three steps: _ROI (Region Of Interest) masking_,_edge detection_ and _line estimation._ First, ROI masking means to reduce the interest area of the original image. The crop image make me focus on the  interest area for lane detection.

​	The second step is the edge detection in the interest image are. For the detection, there are four steps are used: gray scaling, reinforcement of lane color pixel, gaussian filtering, and canny edge detection. The pipeline of gray scaling, gaussian filtering, and canny edge detection  is the general method for the edge detection. However, I proposes to add  the _reinforcement of lane color pixel_ .  The step is to increase the gray scale of the specific region. the region is determined by the colors of lanes. In the project, we have to detect the white and yellow lanes. However, I selected only a yellow color as reinforcement region as following two reasons. The first reason is that  the **white line** can easily be distinguished from **the road (black)** in gray scale. Thus, The reason to select the yellow is that the gray scale of the yellow color is similar to the one of the road (dark gray). Thus, we cannot distinguish the yellow lane from the road in gray scale.

​	The last step is "Line estimation". Based on the edge, we find the potential line segments to construct the lane models. The segments can be searched by hough transform. Next, these lines are divided into two groups: left and right lane groups. Then, we remove the false lines which is placed outside the interest region.  Finally, we make one line model using points of the various line segments using RANSAC. RANSAC is the strong method for linear regression with outlier rejection.




###2. Identify potential shortcomings with your current pipeline

*   The model cannot represent the curved road because the lane model is linear.
*   This algorithm do not include the adaptation on the lightening condition
*   Sometimes, the camera image includes the car hood image. This should be removed.
*   If the road is noisy, canny edge detector does not work well


###3. Suggest possible improvements to your pipeline

*   The lane model may be converted into parametric curve model
*   The threshold values of color masking may be adjusted by the lightening conditions