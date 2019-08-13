---
layout: post
title: Brief Summary of Camera Calibration
---
 

 > Here is a useless guide to camera calibration.
 
 ![Image result for photographer stock image](https://c8.alamy.com/comp/GDB8H4/happy-one-indian-cameraman-photographer-camera-clicking-picture-photography-GDB8H4.jpg)
_<p>WTF are <strong>Camera Extrinsics and Intrinsics</strong>?</p>_
<ul>
<li><p>understanding and mapping the geometry of the scene (4 coordinate systems)</p>
<ul>
<li>world coordinate system (3D)</li>
<li>camera coordinate system (3D)</li>
<li>image plane coordinate system (2D)</li>
<li>sensor coordinate coordinate system (2D)</li>

</ul>
</li>

</ul>
<ul>
<li><p><u>Goal</u>: convert 3D world coordinates to 2D sensor coordinates and back</p>
<ul>
<li>world/object \rightarrow camera \rightarrow image \rightarrow sensor \rightarrow sensor\, (error\,elimination)</li>

</ul>
</li>
<li><p><em>Extrinsics</em>: world/object \rightarrow camera part of transformation</p>
<ul>
<li>pose of camera in the world</li>

</ul>
</li>
<li><p><em>Intrinsics</em>: camera \rightarrow\ldots\rightarrow sensor part of transformation</p>
<ul>
<li>mapping of the scene in front of the camera to the pixels in the final image</li>

</ul>
</li>
<li><p>Transformations are invertible to we can learn about the world from the image as well</p>
</li>

</ul>
