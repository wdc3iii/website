---
layout:     post
title:      Learning for Layered Safety-Critical Control with Predictive Control Barrier Functions
author:     Will Compton
tags: 		Research Hopper
subtitle:  	Conference on Learning for Decisions and Control 2025
category:   paper
thumbnail-img: img/code_background.png
permalink:  /papers/predictive-control-barrier-functions
---
<!-- Start Writing Below in Markdown -->

This post summarizes the content and contributions of my recent paper leveraging simulation, prediction, and learning to achieve safety on complex systems via reduced order modeling, accepted and to be presented at the Conference on Learning for Decisions and Control held in Ann Arbor, Michigan in 2025. We first **motivate** the problem by highlighting the difficulties of achieving safety on complex systems. We then establish a theoretical basis to robustify a control barrier function derived on a reduced order model to achieve safety on the full order model, termed a Predictive Control Barrier Function. Finally, we present a learning algorithm, which improves real-time tractability and enhances sim-to-real transfer via domain randomization. We demonstrate the method on the hopping robot ARCHER. 


The full text of the paper is available from on [arXiv](https://arxiv.org/abs/2412.04658). 

Video...

# Problems with Safety on Complex Systems

# Predictive Control Barrier Functions (PCBFs)

# Learning Predictive CBFs

# Deploying PCBFs on the ARCHER Platform

---

# Learning for Layered Safety-Critical Control with Predictive Control Barrier Functions

**Authors**: **William D. Compton**, Max H. Cohen, Aaron D. Ames

---

## Overview

This paper proposes **Predictive Control Barrier Functions (PCBFs)** — a novel method for ensuring **safe behavior** of **complex systems** by combining **reduced-order models (RoMs)** and **full-order models (FoMs)** with a learned robustness term.

Instead of relying on strict tracking assumptions or overly conservative safety margins, we **learn a minimal correction** term using **massively parallel simulation**, which ensures safety across **both** the RoM and the real-world FoM.

**Key Contributions**:
- Formally prove that Predictive CBFs guarantee safety without strict tracking assumptions.
- Develop a scalable algorithm for **learning** the predictive robustness term.
- Validate the method both in simulation and **experimentally** on the 3D hopping robot **ARCHER**.

---

## Motivation

Designing **Control Barrier Functions (CBFs)** directly for high-dimensional nonlinear systems is difficult.  
Typical layered architectures:
- Synthesize a CBF on a **Reduced-order Model (RoM)**.
- Track the RoM behavior on the **Full-order Model (FoM)**.

**Problem**: Even small tracking errors can cause **safety violations**.

**Solution**: Introduce a **learned robustness correction** — a **Predictive CBF** — that accounts for tracking errors **over a future horizon**, enabling minimal and adaptive constraint back-offs.

---

## Core Idea: Predictive CBFs

Given a CBF on the RoM:
- Predict how tracking errors will evolve.
- Learn a correction term **δ(x)** that minimally adjusts the CBF constraint.
- Guarantee **formal safety** on the FoM without requiring strict tracking assumptions.

We achieve this by:
- Simulating many rollouts of the FoM.
- Learning δ(x) from these rollouts using a **structured supervised learning algorithm**.
- Deploying δ(x) at **real-time rates** on hardware.

![Predictive CBF Architecture](predictive_cbf_diagram.png)

---

## Learning Predictive CBFs

To make PCBFs practical:
- **Massively parallel simulation** (IsaacGym) is used to generate huge datasets.
- A **neural network** is trained to predict δ(x), ensuring:
  - **Minimal conservatism** (tight tubes).
  - **Real-time deployment** (100 Hz on hardware).

Algorithm:
- Roll out system trajectories.
- Measure safety constraint violations.
- Train a network to predict the minimal correction needed to maintain safety.

![Learning Process](learning_process_diagram.png)

---

## Experimental Validation on ARCHER

Deploying the learned Predictive CBF on **ARCHER**, a 3D hopping robot:
- Navigate cluttered environments without collisions.
- Achieve safe behavior where **naive CBFs fail**.
- Maintain real-time operation with **fast evaluation**.

Comparison to naive safety filters:
- **Nominal RoM CBF**: unsafe due to unmodeled tracking errors.
- **Predictive CBF (Learned or Optimized)**: consistently safe.

![ARCHER Navigation Results](archer_navigation_results.png)

---

## Key Insights

- **Prediction horizon** improves safety margins adaptively based on trajectory.
- **Learning** enables scaling to complex systems and hardware imperfections.
- Predictive CBFs **recover and outperform** traditional CBF pipelines, without needing strict assumptions.

---

## Limitations

- Learning still depends on **simulation accuracy** (domain randomization helps).
- **Training time** is substantial (but once trained, evaluation is extremely fast).

---

## Conclusion

Predictive Control Barrier Functions (PCBFs) offer a powerful new way to guarantee safe control of complex systems by:
- Combining reduced-order modeling, predictive simulation, and learning.
- Enabling real-time, adaptive, and provably safe behaviors on challenging hardware platforms.

---

## Learn More

- [Full Paper (arXiv)](https://arxiv.org/abs/2412.04658)
- [Project Video on YouTube](https://youtu.be/6pY7T6yucBs)

