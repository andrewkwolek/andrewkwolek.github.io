---
layout: project
title: Underwater SLAM with BlueROV2
date: January 7, 2025
video: /public/videos/bluerov2.mp4
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
---

## Overview

Underwater SLAM with the BlueROV2 by Blue Robotics is my ongoing winter project as part of the Master of Science in Robotics program at Northwestern University. In this project, I am integrating the BlueROV2 with the Ping360 Scanning Sonar and developing a custom package that runs SLAM alongside the open-source middleware provided by Blue Robotics, BlueOS. The application runs as a Docker container on the Raspberry Pi B4, the onboard computer for the BlueROV2, and integrates data from the IMU, pressure sensor, attitude sensors, and sonar.

Telemetry data is transmitted through the MAVLink protocol, while sonar data is fed directly to the onboard computer. All of the data is sampled and time-synchronized to accurately estimate the ROV’s position and build a map of the surrounding environment. This project is still in progress, and I’m excited to see how it develops!

## Assembly

The first step of the project was assembling the ROV, which involved building the frame, installing six thrusters, setting up the electronics enclosure, connecting the tether, and integrating the camera, sonar, and several other components. The assembly took around 8 hours and required great care and precision to avoid damaging the internal electronics or causing any leaks in the watertight enclosures.

<div class="media-container">
  <video class="responsive-video" autoplay loop muted playsinline>
    <source src="/public/videos/rov_assembly_2of3.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
</div>

More to come!