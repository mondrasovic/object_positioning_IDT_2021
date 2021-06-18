# IDT 2021 - Paper presentatation lecture notes

## Introduction

* In our work, we focused on position estimation of static objects using just a single,  uncalibrated, moving camera.
* Without loss of generality, we narrowed our focus down to road sign position estimation using a single camera attached to a moving vehicle. In the real world, we exploit the GPS camera position captured during the video recording to compute the unknown position of the visible road sign.
* With this in mind, our task can be described as follows. Given only a single, uncalibrated, moving camera and its GPS position in the world... What is the position of the visible road sign delineated by a bounding box in an image?
* The reason why I am repeating the words single, uncalibrated, and moving is the fact that our main contribution is a method for estimating object position with no special hardware required. Moreover, mathematics is easy to implement and is computationally inexpensive.

## Preliminaries

* As a matter of fact, we developed two mathematical approaches both of which can be used to estimate position. However, they vary in the underlying mathematics. Nevertheless, the general principle behind the workings of our two methods remains the same... Is the **triangulation**. As you can see on the screen, the changing position of the camera while still observing the target object may be used to establish a virtual triangle in the scene. Thus, the core principle is to exploit two different views of the same object from two different positions in the world.
* Speaking of different views of some object in conjunction with the triangulation, we need angles. How to obtain them? Well, we decided to approximate them. We acknowledge the slight inaccuracy caused by camera reprojection and distortion. Nonetheless, pragmatically speaking, our computations are sufficient. The angle under which the object is visible is determined by the position of the center of the bounding box with respect to the center of the whole frame.

## Methodology

* Let me introduce you to the first of our methods dubbed **Lines Intersection Method**. In the following slides, I will refer to it as **LIM**. The core idea is analogous to tracing a ray at the object of interest through the optical center of the camera from two different positions. Subsequently, the point of intersection is computed to obtain the object position.
* The second of our methods is the **Law of Sines Method**, abbreviated as **LSM**. As the name suggests, the construction of a triangle in a scene stands at the core of this approach. We exploit the law of sines to compute the length of one side of a triangle given two other angles.

## Dataset creation

## Experiments

## Conclusion
