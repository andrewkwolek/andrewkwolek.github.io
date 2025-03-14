---
layout: project
title: Underwater SLAM with BlueROV2
date: March 14, 2025
video: /public/videos/FullDive.mp4
featured: true
repo: https://github.com/andrewkwolek/BlueOSSLAM
skills:
    - Python
    - Visual Odometry
    - SLAM
    - REST API
    - Concurrency
    - Sonar
    - Telemetry
    - Uvicorn
    - Docker
    - OpenCV
---

## Overview

Underwater SLAM with the BlueROV2 by Blue Robotics is my ongoing winter project as part of the Master of Science in Robotics program at Northwestern University. In this project, I am integrating the BlueROV2 with the Ping360 Scanning Sonar and developing a custom package that runs SLAM alongside the open-source middleware provided by Blue Robotics, BlueOS. The application runs as a Docker container on the Raspberry Pi B4, the onboard computer for the BlueROV2, and integrates data from the IMU, pressure sensor, attitude sensors, and sonar.

Telemetry data is transmitted through the MAVLink protocol, while sonar data is fed directly to the onboard computer. All of the data is sampled and time-synchronized to accurately estimate the ROV’s position and build a map of the surrounding environment. This project is still in progress, and I’m excited to see how it develops!

## Assembly

The first step of the project was assembling the ROV, which involved building the frame, installing six thrusters, setting up the electronics enclosure, connecting the tether, and integrating the camera, sonar, and several other components. The assembly took around 8 hours and required great care and precision to avoid damaging the internal electronics or causing any leaks in the watertight enclosures.

<div style="display: flex; justify-content: center; align-items: center; height: 100vh;">
  <video 
    autoplay 
    loop 
    muted 
    playsinline 
    preload="metadata"
    webkit-playsinline
    style="width: 500px; height: auto;">
    <source src="/public/videos/rov_assembly_2of3.mp4" type="video/mp4">
    <source src="/public/videos/rov_assembly_2of3.webm" type="video/webm">
    Your browser does not support the video tag.
  </video>
</div>

## Data Processing

The BlueROV2 operates on an advanced middleware system called BlueOS, which manages key functions like autopilot, telemetry, camera streams, and external sensors, among others. Although BlueOS is robust in many areas, it lacks a built-in, reliable infrastructure for receiving and processing essential sensor data in real-time—crucial for effective SLAM. To address this, I developed a multithreaded hardware abstraction layer using Python’s asyncio and Docker’s virtualization. This system efficiently collects and processes sensor data in real-time via UDP ports, with three dedicated threads handling Mavlink, camera, and sonar data. The result is streamlined access to the latest sensor data for any application that requires it.

## Visual Odometry

Localizing a vehicle in fluid environments is far more complex than for its wheeled counterparts. Wheeled vehicles benefit from odometry, which allows for a straightforward mapping between wheel rotation and displacement—assuming minimal slippage. Combined with an IMU or other position-estimating sensors and some filtering mechanism, this provides a robust localization model. Unfortunately, vehicles like drones and ROVs don’t have this advantage since they operate in air and water, where there is no direct correlation between propeller rotation and vehicle displacement. As a result, purely mathematical localization is insufficient.

To overcome this, drones rely on visual odometry, a technique that uses cameras and feature detection to track movements in defined objects across consecutive frames. By analyzing the pixel displacement of key features and factoring in the camera's extrinsic parameters, it's possible to estimate the camera's movement by calculating how these features shift within the video stream. I implemented visual odometry by customizing an open-source package to suit my data and improving the feature detection algorithm for more accurate results.

<div style="display: flex; justify-content: center; align-items: center; height: 100vh;">
  <video 
    autoplay 
    loop 
    muted 
    playsinline 
    preload="metadata"
    webkit-playsinline
    style="width: 700px; height: auto;">
    <source src="/public/videos/WallVO.mp4" type="video/mp4">
    <source src="/public/videos/WallVO.webm" type="video/webm">
    Your browser does not support the video tag.
  </video>
</div>



Although this approach succeeded in certain directions, the visual odometry model wasn’t accurate enough to be fully reliable on its own. The BlueROV2 is equipped with a monocular camera, which presents challenges due to its inability to scale movements. Unlike stereo cameras, monocular cameras can’t detect depth, so small pixel noise can be interpreted as large movements, resulting in a noisy model. For monocular visual odometry to work effectively, it requires a feature-rich environment, slower image sampling speeds, and significant computing power.

## Map Generation with Sonar

Due to the challenges of using cameras underwater, sonar is the preferred tool for object detection, mapping, and localization in underwater vehicles. The BlueROV2 is equipped with a Ping360 Scanning Sonar, which can be controlled via an API and a custom communication protocol. In my setup, I utilized the sonar to scan at two different ranges: a 60-degree sweep to simulate forward scanning sonar, and a 360-degree sweep for complete mapping. After generating the sonar image, I apply an adaptive filtering technique to eliminate noise below a defined threshold, followed by spatial clustering to detect key features. The filtered map is then transformed into a 2D point cloud, which serves as a costmap.

<p float="left">
  <img src="/public/images/SonarScan.png" alt="Image 1" width="470"/>
  <img src="/public/images/PointCloud.png" alt="Image 2" width="420"/>
</p>
