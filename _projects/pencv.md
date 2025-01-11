---
layout: project
title: Pen Snatcher
date: September 25, 2024
video: /public/videos/pencv.mp4
featured: false
repo: https://github.com/andrewkwolek/PenCV
skills:
    - Python
    - Feedforward P Controller
    - Rigid-body Motions
    - Computer Vision
    - Multiprocessing
---

## Overview

The Pen Snatcher project integrated computer vision and robotic manipulation to enable the PincherX 100 robot to autonomously grab a purple pen placed in front of it. Using a RealSense camera, the system detected the pen and translated its position from the camera's coordinate system to the robot's frame of reference.

To achieve this, a multi-step calibration process was necessary whenever the workspace was adjusted. The calibration involved moving the robot through various poses while holding the pen, recording both the position of the robot's end effector and the pen's centroid in the camera frame at each pose. These positions were then normalized, and a translation matrix was derived to convert coordinates from the camera frame to the robot's frame.

Once calibration was complete, the program used the real-time position of the pen in the camera frame to guide the robot’s gripper. When the error between the predicted and actual pen position fell below a specified threshold, the robot successfully grabbed the pen and retrieved it from the user.
