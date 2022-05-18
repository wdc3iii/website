---
layout:     post
title:      Semester 7 Prosthesis Research Wrap-Up
author:     Will Compton
tags: 		Research Prosthesis
subtitle:  	Summary of Research and Impact at EPIC Lab
category:   undergraduate
---
<!-- Start Writing Below in Markdown -->

# Table of Contents

* TOC
{:toc}


# Overview
This semester's research work focused primarily on the implementation and testing of the real-time machine learning pipeline.  Additionally, some progress was made towards the beginnings of the adaptive pipeline.  This post builds directly off of previous posts (Semesters [3](), [4](), [5](), [6](), and [7]()), which may introduce vocabulary or topics relevant to this post.  As usual, because of the sensitive nature of active research which is not entirely mine, I can only give overviews here, and will not be sharing any results or code unless the lab has published a paper or open-sourced a codebase.

# Machine Learning Team
The primary focus of the machine learning team was the training and testing of regressors to estimate the speed at which a subject is walking and the angle of inclination of the surface they are walking on, as well as a classifier to recognize the intent to change ambulation modes (i.e. from level walking to ramp ascent).  To train models to perform these tasks, we ran the following experimental protocol.  First, baseline data must be collected across various static walking speeds using the same static assistance parameters.  Walking speeds trials are recorded for 60 seconds, where the treadmill speed is held constant at speed selected from 0.3 to 0.9 m/s in 0.2 m/s intervals.  After these static trials have been collected, two dynamic trials are collected, each in the range of 1.5-2 minutes long.  In the dynamic trials, the treadmill speed is varied according to some predefined speed profile; one is a series of static speeds appended to one another, and the other is a constant speed increase from the minimum to the maximum and back down, as shown in Figure 2.  Similarly, a total of 12 trials are collected on the slope portion of the terrain park, shown in Figure 3, with the inclination of the ramp at each of 7.8°, 9.2°. 11.0°, and 12.4°.  These trials contain both slope information and mode change information.
With the training data collected, speed, slope and mode models are trained.  For this analysis, [Extreme Gradient Boosting](https://machinelearningmastery.com/gentle-introduction-xgboost-applied-machine-learning/) (XGBoost, or XGB) is used.  XBG is a tree-based model which relies upon hand-crafted features to either classify or regress to a specific target.  These features are collected by applying statistical transformations to data from each sensor in a 500ms window.  Features are reported at a 20ms interval, each report of features triggering a prediction.  The sensors onboard the leg (as described more in detail [here]()) are a 6-axis loadcell, thigh, shank, and foot IMUs, and knee and ankle encoders.  
With the models trained, the models are deployed on the leg in a future set of trials, where the accuracies of the models are tested in real-time.  In general, subject dependent models (models trained only on data from the subject) outperform subject independent models (models trained on a group of subjects *other* than the one being tested) and offline results are better than online (real-time) results.  In general, these results agree with theory; a paper on this topic is currently in the works, and when published will be linked here.  

The adaptive machine learning team is looking to come up with ways to improve the accuracy of subject independent models with subject dependent data, as the data is collected in real-time.  To do this, backwards estimators, or a-causal regressors (which are typically more accurate than forwards predictors, or causal regressors) are used to label data as it is collected.  This labeled data is then used to train the forwards predictors or causal regressors.  This is a bit of a nuanced topic, which will be treated more rigorously in a future post ([here]()) as this will be more of a focus in future semesters.  For now, some initial work on the backwards estimators and a-causal regressors has been done, and the adaptive logic has been outlined to put into the leg firmware.  This will be a more immediate focus in coming semesters.  

# Biomechanics Team
The biomechanics team played a key role this semester; we collected motion capture data via the Vicon cameras, and from this motion capture computed joint kinematics, dynamics, and power using [OpenSim](https://simtk.org/projects/opensim).  The data was taken from all of the real-time trials, as well as additional datasets taken with a passive prosthesis.  From this data, the biomechanics team ran comparisons between the active, passive, and able-bodied results, evaluating mostly stride symmetry and power metrics.  The biomechanics data was reporting a significant lack of power from the OSL's ankle joint; as it turns out, an inspection of the firmware revealed a torque coefficient which had been mistakenly set to zero (instead of 1), causing the ankle actuator to produce no torque.  This mistake was corrected, and it's impact on the previously collected data is currently being analyzed.  

# Development Team
The development sub-team focused primarily on obtaining completely wireless operation of the OSL, with all machine learning capabilities being performed on the Raspberry Pi controlling the prosthesis.  Over the course of the semester, the team found that running even just machine learning prediction on the Raspberry Pi created delays within the prosthesis control code, degrading performance.  The current solution is to migrate to a Jetson Nano, with significantly more computational power, in hopes of mitigating these delays.  The team began the development tasks associated with using the Jetson instead of the Raspberry Pi.  

# Conclusion and Next Steps
The primary developments this semester were advances in real-time application of machine learning in control, as well as identification of the torque-scaling error by the biomechanics team.  Future work will include formalizing RT ML results into a paper, pushing into the adaptive machine learning pipeline, and integrating the Jetson Nano with the prosthesis for higher compute capabilities.  