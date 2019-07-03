
--- 
layout: post
title: A Brief Summary of Extrinsics and Intrinsics
---

 > Here is a useless guide to camera calibration.
 
 ![Image result for photographer stock image](https://c8.alamy.com/comp/GDB8H4/happy-one-indian-cameraman-photographer-camera-clicking-picture-photography-GDB8H4.jpg)
 - WTF are **Camera Extrinsics and Intrinsics**?_

  - understanding and mapping the geometry of the scene (4 coordinate systems)
    - world coordinate system (3D)
    - camera coordinate system (3D)
    - image plane coordinate system (2D)
    - sensor coordinate coordinate system (2D)

  - <u>Goal</u>: convert 3D world coordinates to 2D sensor coordinates and back
    - $world/object \rightarrow camera \rightarrow image \rightarrow sensor \rightarrow sensor\, (error\,elimination)$
  - *Extrinsics*: $world/object \rightarrow camera$ part of transformation
    - pose of camera in the world
  - *Intrinsics*: $camera \rightarrow\ldots\rightarrow sensor$ part of transformation
    - mapping of the scene in front of the camera to the pixels in the final image
  - Transformations are invertible to we can learn about the world from the image as well
