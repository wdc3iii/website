---
layout:     post
title:      Caltech Control and Dynamical Systems Qualifying Exams
author:     Will Compton
tags: 		Exams ReferenceMaterials
subtitle:  	Content and Preparation
category:   graduate
---
<!-- Start Writing Below in Markdown -->
# Table of Contents

* TOC
{:toc}

# Introduction

For Caltech Control and Dynamical System (CDS) PhD students, Qualifying Exams are taken at the end of the second quarter and cover the following topics:

- One of: CMS 117 (Probability Theory) or CMS 122 (Mathematical Optimization)
- CDS 131 (Linear Systems)
- CDS 232 (Nonlinear Dynamics)

The structure of the exams is as follows: the student is given a paper exam consisting of three sections (corrosponding the the subjects listed above). Each section of the exam is written by that year's instructor of the corrosponding course. The parts typically have around 3 questions (with possible subquestions). The student is given one hour and thirty minutes to prepare, and then one hour to present solutions to the proctors (made up of some subset of professors in the CDS department). The solution presentation is done on the whiteboard, and is sort of 'adaptive difficulty' - the proctors will ask questions probing the edge of the student's understanding. This can be guiding questions if the subject matter is difficult, or challenging questions (potentially going beyond the written exam) if the original question is handled with ease.

Each section of the exam must be independently passed. Grades given on each section are selected from pass, conditional pass (passing, but may require additional action such as TAing the class a following year) and fail. Sections which are failed must be retaken at the beginning of the summer. The fail rate historically hovers around 1/3 (for each subject), but on the second attempt students almost always pass (at least conditionally). I was lucky enough to pass all three sections on my first attempt, and I chose CMS 122 for my first section.

# Mathematical Optimization (CMS 122)

The optimization course (taught to me by Dr. Venkat Chandrasekaran) focuses heavily on geometric understanding of convexity and duality, including both Fenchal and Lagrange duality schemes. Additionally, the course deals with formulating optimization problems in specfic convex forms, including Linear Programs, Quadratic Programs, Cone Programs, and Semi-Definite Programs. Towards the end of the course, an array of additional concepts are covered, including some introductory (general) numerical methods (such as projected gradient descent), as well as integer programming. The course draws heavily on a sound background in linear algebra (especially properties of matrix decompositions and the geometry of linear spaces and linear systems) and mathematical proof techniques. 

The course follows heavily the context from Boyd and Vandenberghe's [*Convex Optimization*](https://web.stanford.edu/~boyd/cvxbook/). This book notably misses the concept of Fenchal Duality (which is best treated from Venkat's course notes), and may be a bit short for integer programming, where [*Integer Programming*](https://link.springer.com/book/10.1007/978-3-319-11008-0) may be a better reference. While a bit older, [*Convex Analysis*](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://convexoptimization.com/TOOLS/AnalyRock.pdf&ved=2ahUKEwitzLbSxdqIAxViLTQIHWBbFB4QFnoECBMQAQ&usg=AOvVaw0XiiFSd-wgoSbJvOPviK6D) is another decent resource. 

# Linear Systems (CDS 131)

Linear systems, taught to me by Dr. Soon-jo Chung, covers the fundamentals of linear systems control, at a graduate level. The first portion of the course covers state-space control technqiues, including controllability, observability, LQR, and the Kalman filter. The second portion covers Frequency domain methods and introduces concepts in robust control, including signal and system norms, wellposedness and internal stability, and nominal and robust performance/stability criteria. 

The course draws upon more basic concepts in linear control theory, including transfer function/state space representations, stability analysis of SISO systems, bode plots and the nyquist criterion (for SISO systems), as well as some fundamental proof techniques and linear algebra (Jordan Normal Form, eigenvalues/eigenspaces, ect). 

The course draws most heavily on [*Feedback Systems: An Introduction for Engineers and Scientists*](https://www.cds.caltech.edu/~murray/books/AM05/pdf/am08-complete_28Sep12.pdf) and [*Feedback Control Theory*](https://www.control.utoronto.ca/people/profs/francis/dft.pdf). A more advanced reference can be found in [*Robust and Optimal Control*](https://books.google.com/books/about/Robust_and_Optimal_Control.html?id=RPSOQgAACAAJ). 

# Nonlinear Dynamics (CDS 232)

Nonlinear dynamics, taught to me by Dr. Aaron Ames, covers stability and safety analysis for nonlinear systems, and periodic orbits. The fundamental tool of the comparison lemma is used to construct Lyapunov stability analysis and Barrier functions for safety analysis. The end of the course treats periodic orbits, and analyzes their stability in a similar way. 

The course does an excellent job standing alone, and is almost entirely self contained. Control of linear systems, particular state space methods, will benefit the student, as well as some knowledge of real analysis (comfort with epsilon-delta style proofs, sequences, differentiability of multivariate functions). Students interested in integrating the course with topics in geometry (differential manifolds, ect) can extend course content in meaningful ways. 

The course primarily works from Dr. Ames' course notes. However, several supplemental texts are provided, including Khalil's [*Nonlinear Dynamics*](https://www.amazon.com/Nonlinear-Systems-3rd-Hassan-Khalil/dp/0130673897), Sastry's [*Nonlinear Systems*](https://link.springer.com/book/10.1007/978-1-4757-3108-8), and the slightly more advanced, Isidori, [*Nonlinear Control Systems*](https://link.springer.com/book/10.1007/978-1-84628-615-5).

# Study Materials/Techniques

There are several study materials and opportunities provided to Caltech CDS students to prepare for the qualifying exams. Firstly, as exam content is written by the instructor, the materials for the course (homeworks, exams, course notes) are excellent study materials. Additionally, a Google Drive containing recent practice exams is located [here](https://drive.google.com/drive/folders/1YpIiN-Blaow6PZ7Nu8ZrmE2rjH_iapkP?usp=drive_link). It is recommended to save these exams until the end of studying, as there are only four of these exams; they are likely most effective if taken under test-like conditions (under time limits, with an oral presentation at the whiteboard). Additionally, CDS students from years above volunteer to proctor practice exams, so it is best to save one or two of the practice exams for CDS student proctoring. 

# Conclusion
The CDS qualifying exams cover topics which take an applied mathematical perspective on topics in convex optimization, linear control and nonlinear systems theory. These courses are certainly taught in their own way, focusing on some different things from other courses at other institutions; but they do provide a decent starting point for research in the field of control theory. For those interested in applications of control to, say, robotic or aircraft systems, I would recommend looking more into algorithmic/constructive methods for many of these classes. Notable gaps in the coursework include optimization based controllers (MPC, ect), learning based controllers (RL, ...), and to rigorous treatment of estimations. The Caltech courses on Optimal Control and Estimation (CDS 112 my year, now 212), Adaptive Control (CDS 145), and Data Driven Control (CDS 245) fill in some, but not all, of these gaps, and tend to focus on more practical, rather than mathematical, material. 