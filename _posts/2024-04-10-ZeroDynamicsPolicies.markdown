---
layout:     post
title:      Constructive Control of Underactuated Systems via Zero Dynamics Policies
author:     Will Compton
tags: 		Research Control
subtitle:  	Control and Decisions Conference 2024
category:   paper
thumbnail-img: img/code_background.png
permalink:  /papers/zero-dynamics-policies/
---
<!-- Start Writing Below in Markdown -->

This post summarizes the content and contributions of my recent paper on zero dynamics policies, accepted and presented at the Control and Decisions Conference held in Milan, Italy in 2024. We first **motivate** the problem by investigating the difficulty of constructing outputs with stable zero dynamics for underactuated systems, then demonstrate a **constructive** method for synthesizing these outputs on linear systems, a control methodology we denote a **zero dynamics policy**. Similarity between the linear and nonlinear system about the equilibrium allows this method to be be applied to nonlinear systems, and we finish by proposing a **learning method** to construct zero dynamics policies with larger regions of attraction.

The full text of the paper is available from [IEEE](https://ieeexplore.ieee.org/abstract/document/10886411), or on [arXiv](https://arxiv.org/abs/2408.14749). 

The presentation, given at CDC 2024, is available [here](link_to_ppt).

---

# Motivation for Zero Dynamics Policies: Stabilizing Underactuated Systems

# Constructing Zero Dynamics Policies from the Linearization

# Local Zero Dynamics Policies for Nonlinear Systems via Linearization

# Learning Zero Dynamics Policies via Optimal Control


## Overview

This paper proposes **Zero Dynamics Policies (ZDPs)** as a **constructive method** for stabilizing **underactuated nonlinear systems**, like legged robots and manipulators.

The key idea is to **learn a mapping** from the **underactuated coordinates** (the "zero dynamics") to the **desired actuated coordinates**, creating a **controlled invariant** and **stable manifold**. Stabilizing this manifold via output tracking guarantees **stability of the full system**.

**Key Contributions**:
- Proved existence of ZDPs around the origin for any locally controllable system.
- Developed a method to **construct** ZDPs analytically using linearization.
- Introduced a **learning-based approach** using optimal control to extend the region of attraction.
- Demonstrated superior performance compared to LQR on the **nonlinearly damped cartpole**.

---

## Motivation

Traditional methods like input-output linearization and Hybrid Zero Dynamics (HZD) often rely on guesswork or restrictive assumptions.  
**Zero Dynamics Policies** instead **treat outputs as learnable objects**, directly designing a manifold where:
- The system's unactuated dynamics are **stable**.
- The manifold is **controlled invariant** (i.e., reachable via feedback).

This shifts the challenge from guessing outputs to **constructively learning** them using **optimal control and machine learning**.

---

## Core Idea: Zero Dynamics Policies

We define a differentiable mapping:

```
ψ: underactuated state z → desired actuated state η
```

which induces a **zeroing manifold**:

```
Mψ = { (η, z) | η = ψ(z) }
```

The system's dynamics on this manifold (the "zero dynamics") must be:
- **Stable** (trajectories converge).
- **Invariant** under optimal control.

By stabilizing output tracking to this learned manifold, the **full nonlinear system** is guaranteed to stabilize.

![ZDP Concept Diagram](zero_dynamics_policy_diagram.png)

---

## Key Theoretical Results

- **Existence Proof**:  
  For any locally controllable nonlinear system, a ZDP can be **constructed around the origin** using system linearization.

- **Composite Stability**:  
  Stabilizing the output tracking error to zero **implies** full-state stability if the zero dynamics are stable.

- **Learning ZDPs with Optimal Control**:  
  By formulating an optimal control problem (e.g., infinite horizon LQR), ZDPs can be learned to **maximize region of attraction** beyond what linear methods achieve.

---

## Experimental Validation

We validated the approach on the **cartpole** with **nonlinear damping**.

Compared to a standard LQR controller:
- ZDPs **stabilized larger regions of initial conditions**.
- ZDPs exhibited **smoother** and **faster** convergence.
- LQR struggled with oscillations due to unmodeled nonlinearities.

![Cartpole Experiment Results](cartpole_experiments_results.png)

**Training Details**:
- **Policy**: 2-layer feedforward neural network (256 units, ReLU activations).
- **Controller**: Stabilization via simple PD control.
- **Optimization**: iLQR used to approximate optimal trajectories.

[Project Code on GitHub](https://github.com/ivandariojr/LearnedZeroDynamicsPolicies)

---

## Limitations

- Local guarantees require **small neighborhoods** around the origin.
- Learning globally stabilizing policies remains **computationally expensive** (optimal control at every training step).
- Assumes **perfect output tracking** during execution (minor modeling gap).

---

## Conclusion

Zero Dynamics Policies (ZDPs) offer a **constructive, general method** for stabilizing underactuated nonlinear systems by:
- Explicitly learning a stable, invariant manifold.
- Separating the design into **offline learning** and **online tracking**.

This framework bridges **classical nonlinear control** and **learning-based methods**, with promising applications in robotics and beyond.

---

## Learn More

- [Full Paper (arXiv)](https://arxiv.org/abs/2408.14749)
- [Project Code on GitHub](https://github.com/ivandariojr/LearnedZeroDynamicsPolicies)

