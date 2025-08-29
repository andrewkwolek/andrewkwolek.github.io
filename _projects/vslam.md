---
layout: project
title: Visual SLAM in Dynamic Environments from Scratch
date: August 27, 2025
video: /public/videos/VSLAMthumbnail.mp4
youtube_video: https://www.youtube.com/embed/-a7fVRAk5hQ?si=kj_vy2BbJrqf9hI7
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

## Project Description

Visual SLAM represents one of the fundamental challenges in robotics - how can a robot simultaneously understand where it is in the world while building a map of that world using only visual sensors? This project tackles that challenge by implementing a complete SLAM pipeline that processes RGB-D camera data in real-time to estimate camera poses and construct a 3D landmark map.

The system is designed with a modular architecture featuring separate frontend and backend nodes. The frontend handles real-time visual processing including feature detection, tracking, and pose estimation, while the backend manages the global map, performs bundle adjustment optimization, and maintains data consistency across the entire SLAM pipeline.

What makes this implementation particularly interesting is its focus on dynamic environments and robust feature tracking. Rather than assuming a static world, the system is designed to handle moving objects and changing lighting conditions through advanced outlier rejection and adaptive keyframe selection strategies.

## Technical Implementation

### Architecture Overview

<div style="text-align: center; margin: 2rem 0;">
  <img src="/public/images/DynamicSLAMArchitecture.svg" 
       alt="Dynamic SLAM System Architecture" 
       style="max-width: 100%; height: auto; border-radius: 12px; box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);">
  <p style="font-style: italic; margin-top: 1rem; color: #64748b;">Dynamic SLAM system architecture featuring distributed ROS2 nodes</p>
</div>

The SLAM system follows a distributed ROS2 architecture with two main components:

### Frontend Node
- **Multi-modal Processing**: Synchronized RGB-D image processing with object detection integration
- **Advanced Feature Pipeline**: ORB extraction → depth filtering → descriptor matching → geometric validation
- **Intelligent Keyframe Selection**: Adaptive selection based on tracking quality and temporal criteria
- **Semantic Feature Culling**: Prioritizes matched features while adding high-quality unmatched features for new landmark discovery
- **Robust Pose Estimation**: PnP RANSAC with motion outlier detection and coordinate frame conversion

### Backend Node
- **Semantic Landmark Database**: Category-organized persistent landmark storage with descriptor-based association
- **Sliding Window Optimization**: Ceres-based bundle adjustment with Huber loss robust cost functions
- **Data Association Pipeline**: Multi-stage association using descriptor similarity and reprojection error
- **Map Maintenance**: Automatic landmark pruning and triangulation refinement
- **Real-time Visualization**: Continuous publication of optimized poses and landmark positions

### Technical Challenges Solved

## Key Features

### Core SLAM Capabilities
- **Real-time Visual Odometry**: ORB feature detection and tracking with sub-pixel accuracy
- **Sliding Window Bundle Adjustment**: Ceres Solver-based optimization for robust pose estimation
- **Persistent 3D Mapping**: Efficient landmark management and visualization
- **Keyframe-based Architecture**: Adaptive keyframe selection for computational efficiency

### Semantic Integration
- **YOLO Object Detection**: Real-time semantic labeling of visual features
- **Dynamic Object Filtering**: Automatic exclusion of features from moving objects (people, vehicles)
- **Category-aware Landmark Association**: Improved data association using semantic information
- **Multi-class Mapping**: Separate landmark databases for different object categories

### Technical Highlights
- **Coordinate Frame Management**: Seamless conversion between optical and ROS coordinate systems
- **Robust Feature Matching**: Geometric consistency checks with RANSAC outlier rejection
- **Depth Integration**: Intel RealSense depth camera support for metric scale recovery
- **Loop Closure Ready**: DBoW2 vocabulary integration for place recognition (expandable)

## Results & Impact

The implemented SLAM system successfully demonstrates real-time 6-DOF camera pose estimation and 3D landmark mapping in indoor environments. The system maintains tracking accuracy while building persistent maps that can be visualized in RViz, showing thousands of 3D landmarks.

Key performance metrics include sub-centimeter pose accuracy in controlled environments, real-time operation at camera frame rates (30Hz), and robust tracking through challenging scenarios including rapid motion and partial occlusions.

This project serves as a foundation for more advanced robotics applications including autonomous navigation, augmented reality, and robotic manipulation in unknown environments. The modular design and ROS2 integration make it easily extensible for future research and development.