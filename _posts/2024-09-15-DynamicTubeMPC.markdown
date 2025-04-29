---
layout:     post
title:      Dynamic Tube MPC - Learning Tube Dynamics using Massively Parallel Simulation for Robust Practical Safety
author:     Will Compton
tags: 		Research Hopper
subtitle:  	International Conference on Robotics and Automation 2025
category:   paper
thumbnail-img: img/code_background.png
permalink:  /papers/dynamic-tube-mpc/
---
<!-- Start Writing Below in Markdown -->

This post summarizes the content and contributions of my recent paper on Dynamic Tube MPC, accepted and to be presented at the International Conference on Robotics and Automation 2025, in Atlanta, Georgia. We begin by **motivating** the problem by considering 1) rational of the planner-tracker paradigm and 2) issues with feasibility and conservatism with classical tube MPC. Secondly, we introduce a **learning problem**, leveraging massively parallel simulation to learn tube dynamics, to optimize collision free trajectories for the system. Finally, we **deploy** the method on a hopping robot, ARCHER. 

The full text paper can be found on [arXiv](https://arxiv.org/abs/2411.15350).

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe 
    src="https://www.youtube.com/embed/e-aXDbXGfVQ?si=2Fd_8G59LiZSGWIb&autoplay=1&mute=1" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen 
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;">
  </iframe>
</div>

# Motivating Dynamic Tube MPC: Planner-Tracker Paradigm and Classical Tube MPC

When planning paths in cluttered environments, roboticists have a a few main of tools at thier disposal: graph search methods (including A* on a discrete grid, and RRT to construct a graph, followed by A* to search it), heuristic methods (artificial potential fields, ...) and optimization based methods (model predictive control).
When the state or dynamics of the robot is complicated, for instance in the case of a humaniod robot or a hopping robot, none of these methods are computationally tractible to solve planning problems; even at a few dimensions, the curse of dimensionality indicates that the space will be too large to search through, and too nonlinear, nonconvex, and long horizon to optimize for.
In this case, roboticists will typically turn to a durastically simplified model of the robot to solve the planning problem, typically one of:
 - planar state representation $x \in \mathcal{R}^$, no dynamics (kinematic connectivity only)
 - reduced state representation, simple dynamics (single/double integrator, unicycle)

Whatever plan is created using this model representation, called the **planning model** will then be passed down to a tracking controller, designed to control the **tracking model** to follow the plan. 
The planner-tracker paradigm, quite old in robotics, has been treated quite nicely by some of [Claire Tomlin's work](https://arxiv.org/abs/1703.07373).
Critically, because the planner and tracker do not share the same dynamics, the tracking model **will incur error** when it tracks the plan.
This error can lead to collisions in the environment, if not accounted for correctly.

The easiest and fastest adjustment to account for the model mismatch is the buffer all of the obstacles in the environment by a heuristic margin.
If this margin is large enough, meaning that the true system will stay with a **tube** of this size around the nominal trajectory, then it will avoid collision with the environment; this approach is known as tube model predictive control (Tube MPC) - or more specifically, Fixed Tube MPC.
From a theoretical perspective, if the tracking controller can establish a robust tracking invariant around the nominal trajectory, then planning a trajectory such that the tube, created by buffering the plan by the tracking invariant, lies in the free space gives guaranteed collision free paths.

Insert tubes figure...

However, fixing the size of the tube a-priori can lead to significant issues, namely overly conservative behaviors, or unecessary infeasibility, as shown in the figure above. 
Our key insight is the fact that the size of the tracking tube **typically depends on the trajectory you are trying to track**.
For instance, a drone can track a hover point quite well - however, it will incur larger tracking error if you command it to turn a sharp right angle at maximum speed.
If I want a tracking invariant for both of these behaviors, it will be as large as the biggest errors collected during the most aggressive manuevers - but this tube is incredibly conservative for less dynamic, slower behaviors.
The conservative nature of the tube for slower behaviors can lead to planners either 1) not being able to find a route, or 2) require a large excess of conservative behavior, when an aggressive route to the goal exists.

We propose a method to learn a **dynamic** representation of the tracking invariant tube, which depends on both a **history** of previous errors, and information about the plan being tracked.
This results in smaller tubes for easier to track paths, and larger tubes for more difficult to track paths. 
We then integrate this dynamic tube into a Dynamic Tube MPC planner, which generates plans such that the dynamic tube lies is the free space.
This leads to behaviors where the robot moves at maximum agility when far from obstacles, but slows down to safely navigate narrow gaps and tight spaces, enabling safe and dynamic navigation of cluttered environments.

# Learning Tube Dynamics

# Optimizing Tube Dynamics

# Deployment on the ARCHER Platform

---

**Authors**: **William D. Compton**, Noel Csomay-Shanklin, Cole Johnson, Aaron D. Ames

---

## Overview

We introduce **Dynamic Tube MPC**, a new method for robust, real-time safe navigation of cluttered environments.

Instead of assuming a fixed worst-case tracking error, we **learn how tracking error evolves** based on the specific **actions** taken by a **planning model**. This learned **dynamic tube** is used to plan trajectories where the tube stays safely within the free space, enabling both **agility** and **guaranteed safety**.

**Key Contributions**:
- Leverage **massively parallel simulation** to learn tube dynamics at scale.
- Incorporate **error history** to improve prediction accuracy of tracking bounds.
- Formulate a real-time **Dynamic Tube MPC** that optimizes trajectories while guaranteeing collision avoidance.
- Deploy on the 3D hopping robot **ARCHER**, achieving safe, agile navigation through tight clutter.

---

## Motivation

In traditional planning + tracking hierarchies:
- Planning uses a **simplified model**.
- Tracking tries to follow the plan on the **full-order robot**.

**But**:
- **Tracking error** can lead to collisions.
- Most methods use **fixed worst-case bounds** — overly conservative.

**Dynamic Tube MPC** instead learns:
- How **tracking error depends on the plan**.
- How to adaptively **tighten or loosen** planning based on environment difficulty.

---

## Core Idea: Learning Dynamic Tubes

We predict the **size of the tracking error tube** based on:
- A **history** of past tracking errors.
- The **planned future trajectory**.

Two learning methods:
- **One-shot** prediction: predicts the whole future tube at once.
- **Recursive** prediction: predicts tube step-by-step.

Training uses **massive simulated datasets** (400,000+ trajectories), collected with **IsaacGym** for fast GPU-based parallel simulation.

![Dynamic Tube Concept](dynamic_tube_diagram.png)

---

## Dynamic Tube MPC Formulation

Planning optimizes both:
- The **trajectory** of the reduced-order model.
- The **dynamic tube** predicted along that trajectory.

Constraints:
- The **tube** must stay within free space.
- Aggressive moves => larger tube; conservative moves => smaller tube.

Thus, the planner can **trade off speed and safety in real time** based on obstacle proximity.

---

## Experimental Validation on ARCHER

Deployed in hardware experiments:
- **ARCHER** 3D hopping robot navigates cluttered courses safely.
- Dynamically **slows down** when in tight corridors.
- **Speeds up** in open spaces.

Comparison to traditional tube MPC:
- Dynamic Tube MPC achieves **faster traversal** and **higher success rates** without sacrificing safety.
- Fixed tubes either **failed to solve** the problem or were **extremely slow**.

![Hardware Navigation Results](archer_navigation_results.png)

---

## Key Insights

- **Including error history** significantly improves tube prediction accuracy.
- Dynamic tubes **adjust online**, outperforming fixed worst-case tubes.
- **Real-time planning** achieved at **10 Hz** update rates on hardware.
- **Domain randomization** (e.g., robot mass changes) crucial for sim-to-real transfer.

---

## Limitations

- Training trajectories are **random**, while deployment trajectories are **optimized**; future work could better match training and deployment distributions.
- Training tube models is computationally expensive (but one-time cost).

---

## Conclusion

Dynamic Tube MPC offers a **powerful new framework** for **safe and agile** robot navigation:
- Combines learning, simulation, and control.
- Achieves **adaptive safety margins** in real time.
- Scales to complex high-dimensional robotic systems.

---

## Learn More

- [Full Paper (arXiv)](https://arxiv.org/abs/2411.15350)
- [Project Code on GitHub](https://github.com/wdc3iii/LearningTubesMPC)

