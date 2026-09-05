*****
# Shared
*****
### Shared
*****


*****
# SLAM Seminar
*****

## Problem

The Dual Problem
SLAM solves a fundamental "chicken-and-egg" dependency for mobile autonomous robots operating in unknown environments:
Localization: Requires an accurate map to estimate the robot's current pose.
Mapping: Requires precise robot pose estimates to construct a coherent map.


Given a series of controls 
u
t
{\displaystyle u_{t}} and sensor observations 
o
t
{\displaystyle o_{t}} over discrete time steps 
t
{\displaystyle t}, the SLAM problem is to compute an estimate of the agent's state 
x
t
{\displaystyle x_{t}} and a map of the environment 
m
t
{\displaystyle m_{t}}. All quantities are usually probabilistic, so the objective is to compute

<img width="233" height="33" alt="image" src="https://github.com/user-attachments/assets/ffd0b437-42dc-409e-9f81-8b703633e557" />

<img width="755" height="61" alt="image" src="https://github.com/user-attachments/assets/22902370-6f26-4aba-8c07-a733d7c551c8" />

<img width="730" height="53" alt="image" src="https://github.com/user-attachments/assets/c4b6c80e-776d-4024-aeb2-29c161f296ea" />


Like many inference problems, the solutions to inferring the two variables together can be found, to a local optimum solution, by alternating updates of the two beliefs in a form of an expectation–maximization algorithm.

##
## History

Timeline

1986 - Smith and Cheeseman research on the representation and estimation of spatial uncertainty
1990x - research group of Hugh F. Durrant-Whyte 
1995 - The acronym SLAM in the paper "Localization of Autonomous Guided Vehicles"

1986 – 1990s
Foundations
Smith, Cheeseman, & Durrant-Whyte introduce spatial uncertainty and probabilistic landmark estimation.

2000 – 2007
Filter Era
EKF-SLAM and FastSLAM (Particle Filtering) dominate real-time 2D laser mapping.

2007 – 2018
Graph & Visual SLAM
Transition to Factor Graphs, PTAM, and ORB-SLAM leveraging sparse bundle adjustment

2019 – Present
Neural & Spatial AI
NeRF-SLAM, 3D Gaussian Splatting, and Deep Feature tracking transform dense 3D SLAM.

##
## The Early Filter-Based Era

EKF-SLAM
Maintains joint Gaussian distribution over robot state and landmark positions. Suffers from quadratic state expansion O(N2) as landmarks increase.

FastSLAM (Particle Filter)
Uses Rao-Blackwellized Particle Filtering to decouple landmark positions given robot paths, reducing complexity to O(M log N).

Key Bottlenecks
Linearization errors in Extended Kalman Filters cause inconsistencies, landmark misassociations, and severe map divergence over large trajectories.

##
## Factor Graph Optimization

The Graph-Based Paradigm Shift: Modern SLAM models pose estimation as a factor graph optimization problem rather than a recursive state filter.

Nodes & Edges: Nodes represent discrete robot poses and landmarks; edges represent spatial constraints derived from odometry or visual/LiDAR measurements.

Sparsity Advantage: Nonlinear least-squares solvers (g2o, GTSAM, Ceres) leverage sparse Matrix Factorization (Gauss-Newton / Levenberg-Marquardt) for fast real-time global optimization.

##
## Milestones in Visual SLAM

PTAM (2007)
Introduced keyframe tracking and mapping separation into parallel CPU threads.

ORB-SLAM Series
Gold-standard feature-based architecture supporting Mono, Stereo, RGB-D, and Inertial fusion.

Direct Methods (DSO)
Optimizes photometric error directly over raw pixel intensities without explicit feature extraction.

##
## Core SLAM Pipeline

Front-End Sensor Processing: High-frequency odometry, scan matching (ICP/NDT), feature extraction (ORB/SuperPoint), and IMU pre-integration.
Local Mapping & Tracking: Estimating frame-to-frame motion and managing local keyframes or submaps for immediate tracking stability.
Loop Closure Detection: Identifying previously visited places using visual Place Recognition (DBoW2, NetVLAD) to eliminate accumulated drift.
Global Back-End Optimization: Executing full Bundle Adjustment or Pose Graph Optimization to globally adjust trajectory and map geometry.

##
## Neural & Gaussian SLAM
Next-Gen Spatial AI
The frontier of SLAM is rapidly integrating implicit neural representations and deep geometric learning:

NeRF-SLAM: Uses neural radiance fields for continuous implicit map representation.
3D Gaussian Splatting (3DGS): Explicit real-time Gaussian representations (MonoGS, SplaTAM) for ultra-fast photorealistic map synthesis.
Learned Front-Ends: DROID-SLAM and LightGlue replace hand-crafted heuristics with end-to-end differentiable optical flow and feature matching.

##
## Resources
https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping
##
