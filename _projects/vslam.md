---
layout: project
title: Visual SLAM in Dynamic Environments
date: August 27, 2025
video: /public/videos/VSLAMthumbnail.mp4
featured: true
repo: https://github.com/andrewkwolek/dynamic-visual-slam
category: robotics
skills:
    - C++
    - SLAM
    - ROS2
    - RGB-D Camera
    - OpenCV
    - Bundle Adjustment
    - RANSAC
    - Ceres Solver
    - Feature Detection
authors:
  - Andrew Kwolek
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/-a7fVRAk5hQ?si=kj_vy2BbJrqf9hI7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Overview

I implemented a Visual SLAM (Simultaneous Localization and Mapping) pipeline from scratch using a RealSense RGB-D camera, leveraging capabilities from open-source frameworks and libraries such as ROS2, OpenCV, Ceres Solver, and custom message interfaces. This project was completed as a preliminary step to my final project as part of my MS in Robotics degree at Northwestern University.

## Project Description

Visual SLAM represents one of the fundamental challenges in robotics - how can a robot simultaneously understand where it is in the world while building a map of that world using only visual sensors? This project tackles that challenge by implementing a complete SLAM pipeline that processes RGB-D camera data in real-time to estimate camera poses and construct a 3D landmark map.

The system is designed with a modular architecture featuring separate frontend and backend nodes. The frontend handles real-time visual processing including feature detection, tracking, and pose estimation, while the backend manages the global map, performs bundle adjustment optimization, and maintains data consistency across the entire SLAM pipeline.

What makes this implementation particularly interesting is its focus on dynamic environments and robust feature tracking. Rather than assuming a static world, the system is designed to handle moving objects and changing lighting conditions through advanced outlier rejection and adaptive keyframe selection strategies.

## Technical Implementation

### Architecture Overview
The SLAM system follows a distributed ROS2 architecture with two main components:

**Frontend Node**: Responsible for real-time visual odometry, feature detection using ORB descriptors, feature matching with geometric consistency checks, and keyframe detection based on tracking quality and temporal criteria.

**Backend Node**: Manages the global map state, performs sliding-window bundle adjustment using the Ceres optimization library, maintains persistent landmark storage for mapping, and broadcasts optimized poses through TF2.

### Key Algorithms

**Feature Detection & Tracking**: The system uses ORB (Oriented FAST and Rotated BRIEF) features for robust corner detection and description. Features are tracked across frames using descriptor matching with distance filtering and fundamental matrix-based geometric consistency checks via RANSAC.

**Pose Estimation**: Camera poses are estimated using PnP (Perspective-n-Point) with 3D-2D correspondences between previous frame landmarks and current frame features. The system includes motion outlier detection to reject impossible camera movements and coordinate frame transformations between optical and ROS conventions.

**Bundle Adjustment**: A sliding-window bundle adjustment system using Ceres Solver optimizes camera poses and landmark positions simultaneously. The implementation uses Levenberg-Marquardt optimization with Huber loss functions for robustness against outliers.

**Keyframe Selection**: Intelligent keyframe detection based on tracking quality (number of successfully matched features) and temporal criteria ensures the system maintains good map coverage while avoiding redundant frames.

### Technical Challenges Solved

**Coordinate Frame Management**: Proper handling of transformations between camera optical frames, ROS coordinate conventions, and world frames, ensuring consistent pose estimation and landmark mapping.

**Real-time Performance**: Optimized feature detection with depth masking, efficient descriptor matching, and carefully tuned bundle adjustment frequency to maintain real-time operation.

**Robust Tracking**: Multiple layers of outlier rejection including distance-based feature filtering, fundamental matrix RANSAC, and motion consistency checks to handle dynamic environments and measurement noise.

**Memory Management**: Sliding window approach for bundle adjustment and intelligent landmark pruning to maintain computational efficiency while preserving map quality.

## Results & Impact

The implemented SLAM system successfully demonstrates real-time 6-DOF camera pose estimation and 3D landmark mapping in indoor environments. The system maintains tracking accuracy while building persistent maps that can be visualized in RViz, showing thousands of 3D landmarks.

Key performance metrics include sub-centimeter pose accuracy in controlled environments, real-time operation at camera frame rates (30Hz), and robust tracking through challenging scenarios including rapid motion and partial occlusions.

This project serves as a foundation for more advanced robotics applications including autonomous navigation, augmented reality, and robotic manipulation in unknown environments. The modular design and ROS2 integration make it easily extensible for future research and development.