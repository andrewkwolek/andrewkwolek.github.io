---
layout: project
title: Pen Snatcher
date: September 25, 2024
video: /public/videos/pencv.mp4
featured: true
repo: https://github.com/andrewkwolek/PenCV
skills:
    - Python
    - Feedforward P Controller
    - Rigid-body Motions
    - Computer Vision
    - Multiprocessing
---

## Overview

The Pen Snatcher project integrates computer vision and robotic manipulation to enable the PincherX 100 robot to autonomously grab a purple pen placed in front of it. Using a RealSense camera, the system detects the pen and translates its position from the camera's coordinate system to the robot's frame of reference.

To achieve this, a multi-step calibration process is necessary whenever the workspace is adjusted. The calibration involves moving the robot through various poses while holding the pen, recording both the position of the robot's end effector and the pen's centroid in the camera frame at each pose. These positions are then normalized, and a translation matrix is derived to convert coordinates from the camera frame to the robot's frame.

Once calibration is complete, the program uses the real-time position of the pen in the camera frame to guide the robot’s gripper. When the error between the predicted and actual pen position falls below a specified threshold, the robot successfully grabs the pen and retrieves it from the user.

## Pen Recognition

The first step is to enable the RealSense camera to measure the 3D location of the purple pen. To achieve this, an image processing pipeline is developed that takes the raw camera input and outputs the (x, y, z) coordinates of the pen's centroid in the camera frame.

The process begins by aligning the depth image with the RGB image to capture the full spatial information. Next, RSV filtering is applied to isolate the purple pen, ensuring that it is the only object visible in the image. Once the image is effectively masked, the pipeline identifies the largest contour, which is assumed to correspond to the pen. Finally, the centroid of this contour is calculated, providing the 3D coordinates of the pen's centroid in the camera frame.

## Extrinsic Calibration

Calibration is carried out by placing the pen in the grippers and having the robot move through several poses within its workspace. At each pose, both the position of the pen as measured by the image processing pipeline in the camera frame and the position of the robot's end effector in the robot frame are recorded.

Once enough data points are collected, the centroids of the points in both the camera and robot frames are calculated. Each point is then normalized by subtracting its respective centroid. The rotation matrix between the pairs of points is computed.

After determining the rotation matrix, the translation is calculated by finding the offset between a rotated point from the camera frame to the robot frame and the actual point in the robot frame. Finally, the calibration parameters are saved in a pickle file for future use in controlling the robot.

<video width="640" height="360" loop autoplay muted>
  <source src="/public/videos/calibration.webm" type="video/webm">
  Your browser does not support the video tag.
</video>

## Robot Control

The robot is controlled using a feedforward P controller that tracks the position of the pen's centroid. By leveraging multiprocessing, both the image pipeline and the robot's motion run concurrently. The image processing pipeline captures images and computes the current position of the pen. These coordinates are then placed into a queue, which the robot's motion process receives.

If the coordinates are valid, the robot moves to the corresponding position of the pen. This process continues until the error is reduced below a specified threshold, at which point the grippers close to grab the pen.
