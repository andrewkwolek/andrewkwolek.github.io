---
layout: project
title: Mobile Manipulation
date: December 13, 2024
video: /public/videos/mobilemanip.mp4
featured: false
repo: https://github.com/andrewkwolek/mobile-manipulation
skills:
    - Python
    - Feedforward PI Controller
    - CoppeliaSim
---

## Overview

The **Mobile Manipulation** project applies fundamental principles from *Modern Robotics* by Kevin Lynch, including velocity kinematics, odometry, motion planning, trajectory generation, velocity control, and forward kinematics. The project focuses on planning and executing a trajectory for the end-effector of the **youBot** mobile manipulator, which consists of a mobile base with four mecanum wheels and a 5R robot arm. 

The system performs odometry as the robot chassis moves, uses feedback control to guide the youBot to pick up a block from a specified location, transport it to a target area, and place it down.

Various controllers were tested, each with different levels of overshoot and convergence. Among them, the **Feedforward PI controller** proved to be the most effective for accurate trajectory tracking. The software architecture is built around three core components:

1. **Kinematics Simulator**
2. **Trajectory Generation**
3. **Feedforward Control**

These components were seamlessly integrated within a control loop to enable precise motion and ensure the successful completion of the pick-and-place task.
