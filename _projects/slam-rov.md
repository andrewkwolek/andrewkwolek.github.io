---
layout: project
title: Underwater SLAM with BlueROV2
date: March 19, 2025
video: /public/videos/bluerov2-2.mp4
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

Underwater SLAM with the BlueROV2 by Blue Robotics is my ongoing winter project as a part of the Master of Science in Robotics program at Northwestern University. For this project, I am assembling the BlueROV2 with the addition of the Ping360 Scanning Sonar and implementing my own package that runs SLAM alongside the open source middleware provided by Blue Robotics, BlueOS. The application runs as a Docker container on the Raspeberry Pi B4, the onboard computer for the BlueROV2, and integrates IMU, pressure, attitude, and sonar data. The telemetry data is transmitted through the Mavlink protocol while the sonar data is connected directly to the onboard computer, and all are sampled and timesynced in order to accurately estimate the ROV's current position, and build a map of the surrounding environment. This project is currrently in progress and I am excited to see where it goes!

## Assembly

The first step was assembling the ROV which included the frame, six thrusters, electronics enclosure, tether, camera, sonar, and maany other components. Assembly took about 8 hours and required extreme care and precision to avoid damaging any of the internal electronics coponents and prevent any leaks in the water tight enclosures.

