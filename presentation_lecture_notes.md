# IDT 2021 - Paper presentation lecture notes

## Introduction

* In our work, we focused on **position estimation static objects** using just a **single, uncalibrated, moving camera**.
* Without loss of generality, we narrowed our focus down to **road sign position estimation** using a single camera attached to a moving vehicle. In the real world, we exploit the GPS camera position captured during the video recording to compute the unknown position of the visible road sign.
* With this in mind, our **task can be described** as follows. Given only a single, uncalibrated, moving camera and its GPS position in the world... What is the position of the visible road sign delineated by a bounding box in an image?
* The reason why I am repeating the words single, uncalibrated, and moving is the fact that our **main contribution** is a method for estimating object position with no special hardware required. Moreover, mathematics is easy to implement and is computationally inexpensive.

## Preliminaries

* As a matter of fact, we developed two mathematical approaches both of which can be used to estimate position. However, they vary in the underlying mathematics. Nevertheless, the general principle behind the workings of our two methods remains the same... Is the **triangulation**. As you can see on the screen, the changing position of the camera while still observing the target object may be used to establish a virtual triangle in the scene. Thus, the core principle is to exploit two different views of the same object from two different positions in the world.
* Speaking of different views of some object in conjunction with the triangulation, we need **angles**. How to obtain them? Well, we decided to **approximate them**. We acknowledge the slight inaccuracy caused by camera reprojection and distortion. Nonetheless, pragmatically speaking, our computations are sufficient. The angle under which the object is visible is determined by the position of the center of the bounding box with respect to the center of the whole frame.

## Methodology

* Let me introduce you to the first of our methods dubbed **Lines Intersection Method**. In the following slides, I will refer to it as **LIM**. The core idea is analogous to tracing a ray at the object of interest through the optical center of the camera from two different positions. Subsequently, the point of intersection is computed to obtain the object position.
* The second of our methods is the **Law of Sines Method**, abbreviated as **LSM**. As the name suggests, the construction of a triangle in a scene stands at the core of this approach. We exploit the law of sines to compute the length of one side of a triangle given two other angles.
* If we assume 24 frames per second in a video, and that a road sign may be visible for several seconds, it makes up to a great number of pairs of frames for triangulation. But how to choose which one if the best? Well, we developed a simple statistical approach to **combine multiple elementary position estimates** into a single, **refined position estimate**.

## Dataset creation

* Using a mathematical model without proper empirical testing may be like shooting in the dark. In our case, we decided to exploit the possibilities of **3D modeling**. We created a simulation where a vehicle passes by a road sign in a specifically designed environment. We aimed for ideal testing environment to examine our proposed mathematical model in laboratory conditions.
* However, simulation also allowed us to test the model using **aritificial noise**. You can imagine that there are various sources of noise, such as, camera GPS position or road sign detection.
* On the other hand, what works in theory may fail in practice. Thus, we subjected our equations to rigorous scrutiny of real-world application. To this end, we created a **real dataset** as a recording in a town. One disadvantage was the **frequency of GPS sampling**. It was approximately once or twice per second. Having 24 frames per second required interpolating the GPS positions, and for that purpose we went with linear approximation since the car speed was not really high.
* The biggest source of errors and noise in our data was the **estimation of the ground truth road sign position**. Unfortunately we were not equipped with special hardware. So we were left with a mobile phone GPS signal and Google Street View. We could combine the measuremenets to produce a single position estimate. We included the samples into the dataset only if we were confident enough. We do acknowledge a great deal of **subjectivity** in this step. The real dataset is the major drawback of our work and definitely needs improving.
* Here you can see some **overall statistics** of the composition of our datasets. There is variation in presence or absence of hills, change in elevation and curvature of the road.

## Experiments

* As far as the results of our experiments are concerned, here I present you a visualization of position estimates. Before scaring you off with seemingly highly inaccruate estimate, I encourage you to keep the X and Y axis units in mind. 
## Conclusion
