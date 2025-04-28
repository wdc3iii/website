---
layout:     post
title:      Dynamic Tube MPC - Learning Tube Dynamics using Massively Parallel Simulation for Robust Practical Safety
author:     Will Compton
tags: 		Research Hopper
subtitle:  	International Conference on Robotics and Automation 2025
category:   paper
thumbnail-img: img/code_background.png
---
<!-- Start Writing Below in Markdown -->

This post summarizes the content and contributions of my recent paper on Dynamic Tube MPC, accepted and to be presented at the International Conference on Robotics and Automation 2025, in Atlanta, Georgia. We begin by **motivating** the problem by considering 1) rational of the planner-tracker paradigm and 2) issues with feasibility and conservatism with classical tube MPC. Secondly, we introduce a **learning problem**, leveraging massively parallel simulation to learn tube dynamics, to optimize collision free trajectories for the system. Finally, we **deploy** the method on a hopping robot, ARCHER. 

The full text paper can be found on [arXiv](https://arxiv.org/abs/2411.15350).

Include video...

# Motivating Dynamic Tube MPC: Planner-Tracker Paradigm and Classical Tube MPC

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

