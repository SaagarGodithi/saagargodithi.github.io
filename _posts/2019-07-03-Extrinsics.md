---
layout: post
title: Camera Calibration Sparknotes: Extrinsics
---

 > Here is a useless guide to camera extrinsics.
 
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

- Extrinsics

  - **Parameters ** describe the pose (position and heading) of the camera with respect to the real world.  6 parameters total (3 for position + 3 for heading)
    - The Point $P$ with coordinates in world coordinates 
      - $\boldsymbol{X_P}=[X_P, Y_P, Z_P]^T $
    - The Center $O$ of the projection
      - $\boldsymbol{X_O}=[X_O,Y_O,Z_O]^T$
  - **Transformation** = **translation** + **rotation**
    - $\boldsymbol{^kX_P} = R(\boldsymbol{X_P}-\boldsymbol{X_O})$ [Euclidian]
