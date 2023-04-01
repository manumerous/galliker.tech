---
layout: project
title: 'Data Driven Dynamics Modelling for Unmanned Aerial Vehicles'
caption: Creating a digital-twin from flight logs.
# description: >
#   This is how I use Hydejack on my personal site. 
#   Much of the development is informed from my experience of using it myself, creating a tight feedback loop.
date: 1 Jun 2021
image: 
  path: /assets/img/projects/data_driven_dynamics/tilt_wing_mountains.png
  srcset: 
    1920w: /assets/img/projects/data_driven_dynamics/tilt_wing_mountains.png
links:
  - title: Link
    url: https://github.com/ethz-asl/data-driven-dynamics
accent_color: '#4fb1ba'
accent_image: /assets/img/projects/data_driven_dynamics/tilt_wing_mountains_landscape.JPG
background: '#193747'
theme_color: '#193747'
sitemap: false
---

A dynamics model is a valuable tool for a variety of applications, including simulations and control. However, traditional methods for obtaining such models for an unmanned aerial vehicle (UAV), such as wind tunnel testing or the installation of additional sensors, can be time-consuming, inaccesible and costly. 

In this research project, I aimed to address these challenges by proposing a data-driven dynamics modelling pipeline that uses a unified flight log (uLog) format. The primary objective was to establish a framework for obtaining a dynamics model solely by minimizing the prediciton error of the model with respect to the flight data collected by the by default on the vehicle installed sensors. Initially, a parametric model with nonlinear characteristics was utilized as it provides the ability to measure the degree to which each modeled component manifests within the dataset. However, this can be readily expanded to a model-free or deep learning methodology.

The effectiveness of the proposed framework was investigated on various UAVs, including multirotors and vertical take-off and landing (VTOL) UAVs. Whilst the results were promising, it also became evident throughout the course of my research that an organized methodology for gathering data is paramount to the attainment of a comprehensively generalizable model that faithfully captures the underlying physical phenomena. Especially for fixed-wing and vertical take-off and landing (VTOL) UAVs pose a significant challenge due to their exceedingly nonlinear and unstable behavior near the stall, necessitating the development of specialized flight maneuvers to explore the dynamics beyond their nominal operating point.

The pipeline was published as an open source project and presented at the PX4 dev summit. It provides functionalities to read and select data from the ULog file format, estimate the dynamics model and integrate it into the [PX4 Gazebo flight simulator](https://github.com/PX4/PX4-SITL_gazebo-classic). The process is fully automated for the example of a parametric multi-rotor model, for which the collectied flight data that sufficiently exposes the linear and angular dynamics of the vehicle is relatively simpel. Furthermore, the modular approach of the pipeline allows for easy extension with additional air frames and model structures in the future.

## Overview of the Pipeline

<p align = "center"><img src = "/assets/img/projects/data_driven_dynamics/PipelineDiagramm_bar.png"></p><p align = "center">
<em>Fig.1 - Main building blocks of the data-driven-dynamics pipeline.</em>
</p>