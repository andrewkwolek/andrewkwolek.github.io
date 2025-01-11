---
layout: project
title: Jack in a Box
date: December 14, 2024
video: /public/videos/jack.mp4
repo: https://github.com/andrewkwolek/jackinabox
featured: false
skills:
    - Python
    - Lagrangian Dynamics
    - Animation
---

## Overview

The *Jack in the Box* project is a physics simulation that models the motion of a four-sided jack bouncing inside a box subjected to external forces. Using Lagrangian dynamics, the simulation accurately captures the system's energy, impacts, constraints, and forces, providing a highly realistic representation of real-world behavior. The model incorporates two rigid bodies, six degrees of freedom, and operates in a planar environment, making it a complex system with a high degree of precision and realism.

## Project Setup

To derive the Euler-Lagrange equations for the *Jack in the Box* simulation, I began by calculating the kinetic and potential energies of the box and jack. 

For the **kinetic energy**, I computed the velocity of both the box and jack frames. This was achieved by taking the inverse of the transformation matrix and multiplying it by the time derivative of the transformation matrix. I then "unhatted" the resulting matrices to obtain the velocity components in all 6 degrees of freedom. The kinetic energy was calculated by taking the dot product of the unhatted velocity vector with the Inertia tensor, and then summing the values for both the box and the jack.

For the **potential energy**, I multiplied the y-component of the box and jack’s positions by their respective masses and gravity. The Lagrangian was then derived by subtracting the potential energy from the kinetic energy.

Next, I calculated the Euler-Lagrange equations by computing the following terms:
- $$ \frac{dL}{dq} $$
- $$ \frac{dL}{dq'} $$
- $$ \frac{d}{dt} \left( \frac{dL}{dq'} \right) $$

The right-hand side of the Euler-Lagrange equations was formulated as the difference between $$ \frac{d}{dt} \left( \frac{dL}{dq'} \right) $$ and $$ \frac{dL}{dq} $$, while also adding external forces and constraint equations. The constraints were implemented to ensure that the box remained stationary at the origin, preventing it from falling off the screen during the animation. These constraints were modeled by setting the x- and y-components of the box’s position to zero.

Two **external forces** were applied to the box:
1. A normal force to counteract gravity when the box constraint failed.
2. A torque that gradually increased over time, inducing a slow spin on the box.

For the **impact conditions**, I computed the configuration of the jack in the box frame $$ g_{AB} $$. Using this transformation matrix, I found the positions of the four points of the jack by displacing them along each axis (+x, -x, +y, -y). By multiplying $$ g_{AB} $$ by each point’s vector, I identified their locations in the box frame. To check for impacts, I compared these coordinates against the box’s walls to determine if any jack points exceeded the box’s boundaries.

I calculated the impact equations by evaluating the following:
- The $$ \frac{d\phi}{dq} $$ terms for each of the 16 impact conditions.
- The Hamiltonian of the system, incorporating the impact dynamics.

Finally, at each timestep, I checked whether any impact conditions were violated. If a violation occurred, I used the corresponding update equations to compute the new state and update the configuration array, simulating the impact response.
