# IDT 2021 - Paper presentation lecture notes

## Introduction

* My name is **Milan Ondrašovič** and I am going to talk about **position estimation of static objects** using a **single, uncalibrated, moving camera**.
* Without loss of generality, we narrowed our focus down to **road sign position estimation** using a single camera attached to a moving vehicle. We exploited the GPS camera position captured during the video recording.
* Our **task can be described** as follows. Given only a single, uncalibrated, moving camera and its GPS position in the world... What is the position of the visible road sign delineated by a bounding box in an image?
* Our **main contribution** is a method for estimating object position with no special hardware required.

## Preliminaries

* As a matter of fact, we developed two mathematical approaches both of which can be used to estimate object position. The underlying mathematics is based on **triangulation**. As you can see on the slide, the changing position of the camera while still observing the target object may be used to establish a virtual triangle in the scene. Thus, the core principle is to exploit two different views of the same object from two different positions in the world.
* Speaking of different views of some object in conjunction with the triangulation, we need **angles**. How to obtain them? We **approximated them**. We acknowledge the slight inaccuracy caused by camera reprojection and distortion. Nonetheless, our computations were sufficient. The angle under which the object was visible was determined by the position of the center of the bounding box with respect to the center of the whole frame.

## Methodology

* Let me introduce you to the first of our methods dubbed **Lines Intersection Method**, abbreviated as **LIM**. The core idea is analogous to tracing a ray at the object of interest through the optical center of the camera from two different positions. Subsequently, the point of intersection is computed to obtain the object position.
* The second of our methods is the **Law of Sines Method**, abbreviated as **LSM**. As the name suggests, the construction of a triangle in a scene stands at the core of this approach. We exploit the law of sines to compute the length of one side of a triangle given two other angles.
* If we assume 24 frames per second in a video, and that a road sign may be visible for several seconds, it adds up to a great number of pairs of frames for triangulation. But how do we choose which one is the best? Well, we used simple statistics to **combine multiple elementary position estimates** into a single, **refined position estimate**.

## Dataset creation

* As far as our data were concerned, we decided to exploit the possibilities of **3D modeling**. We created a simulation where a vehicle passed by a road sign in a specifically designed environment. We aimed for an ideal testing environment to examine our proposed mathematical model in laboratory conditions.
* Simulation also allowed us to test the model using **artificial noise**. You can imagine that there are various sources of noise, such as camera GPS position or road sign detection.
* Besides, we also created a **real dataset** as a recording in a town. One disadvantage was the **frequency of GPS sampling**. It was approximately once or twice per second. Having 24 frames per second required interpolating the GPS positions, and for that purpose, we went with linear approximation since the car speed was not high.
* The biggest source of errors and noise in our data was the **estimation of the ground truth road sign position**. Unfortunately, we were not equipped with special hardware. So we were left with a mobile phone GPS signal and Google Street View. We could combine the measurements to produce a single position estimate. We included the samples into the dataset only if we were confident enough. We do acknowledge a great deal of **subjectivity** in this step. The real dataset was the major drawback of our work and needs improvement.
* Here you can see some **overall statistics** of the composition of our datasets. There is variation in the presence or absence of hills, change in elevation, and curvature of the road.

## Experiments

* As far as the results of our experiments are concerned, here I present you a **visualization of position estimates**. Before scaring you off with seemingly highly inaccurate estimates, I encourage you to keep in mind the **units of the X and Y axis**. These scatter plots are to depict the, among other things, negligible difference, between the two developed methods. You can see a bunch of elementary estimates, then the refined estimate marked in orange, and the position of the real object in red.
* The upcoming two plots show the statistics of the accuracy of our methods. Here you can see the **mean accuracy of the position estimation on all of our datasets**. The first five groups belong to synthetic datasets, while the worst-performing one belongs to the real dataset. Concerning the synthetic data, you can see that except for the "*s-left*" dataset in the middle, the performance is pretty much identical. The slight deviation is caused by placing the road sign on the left side of the road. The accuracy is simply measured as the **Euclidean distance** between the ground truth and the estimated 2D positions.
* This slide is the same as the previous one but shows the **standard deviation of the accuracy of our methods** instead of the mean accuracy.
* We also conducted experiments to assess the **influence of distance** on the accuracy of our calculations. The obvious expectation is that the further away the object is from the camera, the more difficult it is to estimate its position precisely. The two plots support these assumptions well. 

## Conclusion

* To **summarize** our contribution, I would say that we focused on the position estimation of a road sign from a single camera attached to a vehicle. We **developed**, **implemented**, and **tested** **two mathematical approaches** that were inherently based on **triangulation**. To test the models, we created a **synthetic** and a **real dataset**. Among other things, we conducted experiments with **artificial noise**. The key takeaway may be that concerning synthetic data, our models achieve accuracy below 1 meter. Conversely, in the real world, it was around 4 meters, according to the data. The developed approaches are **simple to implement** and can be used as supporting computations in situations where extreme accuracy of position estimation is not required.