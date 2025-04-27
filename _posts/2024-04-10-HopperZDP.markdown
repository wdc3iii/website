---
layout:     post
title:      Robust Agility via Learned Zero Dynamics Policies 
author:     Will Compton
tags: 		Research Hopper
subtitle:  	International Conference on Intelligent Robots and Systems 2024
category:   paper
thumbnail-img: img/code_background.png
---
<!-- Start Writing Below in Markdown -->

# Robust Agility via Learned Zero Dynamics Policies

**Authors**: Noel Csomay-Shanklin\*, **William D. Compton**\*, Ivan Dario Jimenez Rodriguez\*, Eric R. Ambrose, Yisong Yue, Aaron D. Ames  
\* Equal contribution

---

## Overview

In this work, we present **Zero Dynamics Policies (ZDPs)** — a new framework for robust and agile control of **hybrid underactuated systems**, with experimental validation on the 3D hopping robot **ARCHER**.

Our method decomposes controller design into two components:
1. **Learning** a mapping from unactuated to actuated coordinates that is invariant under optimal control.
2. **Driving** the actuated coordinates to this learned mapping using a stabilizing controller.

This structure leverages the natural dynamics of underactuation, achieving both **dimension reduction** and **robust stability**, while significantly **reducing online computational burden** compared to full model predictive control.

**Key Results**:
- Over **3000 stable hops** on rough terrain.
- Recovery from large disturbances and blind traversal of rough terrain, including stair-climbing, ramp descending, and narrow-beam hopping.
- **State-of-the-art agility** without requiring vision or extensive replanning.

[![Watch ARCHER in action](archer_hopping_thumbnail.png)](https://vimeo.com/923800815)

---

## Motivation

Legged robots, manipulators, and swimmers are all examples of **underactuated systems**, where not every degree of freedom can be directly controlled. Traditional approaches like **Model Predictive Control (MPC)** and **Reinforcement Learning (RL)** either suffer from high computational cost or require massive data and tuning.

**Zero Dynamics Policies** strike a new balance:  
- Retain **optimality** and **stability** guarantees.
- Focus only on the **unactuated** degrees of freedom.
- Achieve **real-time performance** with a lightweight policy and simple PD control.

---

## Core Idea: Zero Dynamics Policies

We **learn a mapping** (the Zero Dynamics Policy) from the **underactuated states** (e.g., position) to the **desired actuated states** (e.g., orientation).

This learned manifold:
- Is designed to be **invariant** under optimal control actions.
- Has **provably stable** zero dynamics.
- Can be stabilized using lightweight **PD controllers**.

![ZDP Concept Diagram](zero_dynamics_policy_diagram.png)

---

## Experimental Validation on ARCHER

**ARCHER** is a 3D hopping robot with flywheel-based attitude control and a powerful leg actuator.

Using ZDPs, ARCHER achieves:
- **Disturbance rejection** up to 1 mph lateral winds.
- **1.5” stair climbing** and **20° ramp descent**.
- **Narrow beam hopping** across a 2x4.
- **Treadmill hopping** over long distances without failure.

We track the robot’s orientation through a **simple quaternion PD controller** at 1 kHz, applying additional flywheel **spin-down** control during ground contact to maintain actuation effectiveness.

![Hardware Snapshots](archer_experiments_snapshots.png)

---

## Key Metrics

- **3000+ stable hops**.
- **Low drift** from the desired impact conditions across trials.
- **Comparison with LQR** shows ZDPs outperform naive linear controllers in stability and agility.

![Policy Tracking Results](policy_tracking_results.png)

---

## Limitations

- **Training** is computationally expensive (about 2 seconds per iteration for batch size 30).
- **Initialization** requires a reasonable starting policy (e.g., Raibert heuristic).
- **Current application** is focused on discrete-time hybrid systems; extensions to continuous-time remain future work.

---

## Conclusion

**Zero Dynamics Policies** offer a **powerful, generalizable method** for stabilizing hybrid underactuated systems.

By **combining optimal control with structure-aware learning**, we demonstrate both **theoretical guarantees** and **hardware success** — paving the way for future applications to legged locomotion, hopping, and beyond.

**Future Work**:
- Integrating ZDPs with **reinforcement learning**.
- Applying to more complex **multi-legged systems**.
- Extending the approach to **continuous-time hybrid dynamics**.

---

## Learn More

- [Full Paper (arXiv)](https://arxiv.org/abs/2409.06125)
- [Project Code on GitHub](https://github.com/ivandariojr/LearnedZeroDynamicsPolicies)
- [Watch ARCHER hopping!](https://vimeo.com/923800815)
