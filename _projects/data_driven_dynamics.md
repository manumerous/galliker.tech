---
layout: project
title: 'Data Driven Dynamics Modelling for Unmanned Aerial Vehicles'
caption: Creating a digital-twin from flight logs.
# description: >
#   This is how I use Hydejack on my personal site. 
#   Much of the development is informed from my experience of using it myself, creating a tight feedback loop.
date: 1 Jun 2021
image: 
  path: /assets/img/projects/data_driven_dynamics/tilt_wing_mountains_focus.JPG
  srcset: 
    1920w: /assets/img/projects/data_driven_dynamics/tilt_wing_mountains_focus.JPG
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
In this research project, I aimed to address this challeng by proposing a data-driven dynamics modelling pipeline that uses the [PX4 unified flight log (ULog)](https://docs.px4.io/main/en/dev_log/ulog_file_format.html) format. The primary objective was to establish a framework for obtaining a dynamics model solely by minimizing the prediciton error of the model with respect to the flight data collected by the by default on the vehicle installed sensors. The developed pipeline takes a modular approach to ensure adaptability for different model fidelities and airframes, such as multi-rotor, fixed-wing, and VTOL. Specifically, for the example of multirotors, the pipeline automates the joint estimation of the UAV's dynamics model and the quality of the fit and integrates the former into the [PX4 Gazebo flight simulator](https://github.com/PX4/PX4-SITL_gazebo-classic).The data-driven-dynamics pipeline is published as an [open source project on Github](https://github.com/ethz-asl/data-driven-dynamics) and presented at the [Linux Foundation PX4 Developer Summit 2021](https://events.linuxfoundation.org/archive/2021/px4-developer-summit/).

## Overview of the Pipeline

<p align = "center"><img src = "/assets/img/projects/data_driven_dynamics/PipelineDiagramm_bar.png"></p><p align = "center">
<em>Fig.1 - Main building blocks of the data-driven-dynamics pipeline.</em>
</p>

- **Data Processing:** this module loads and preprocesses the data used to estimate the dynamics model. It contains functionalities to filter, resample and normalize the data.
- **Data Selection** Optionally the user has the ability to visualize the data and additional  step to visually select a suportion of the data that is best suited to estimate the dynamics model. 
- **Model Definition** Defines the model structure used to predict the dynamics. The parametric model contains functionalities to make a custom parametric model by specifying the amount of rotors and aerodynamic elements (e.g. wings) that make up the vehicle. 
- **Optimization Framework** Depending on the chosen model 
- **Dynamics Model Output** Description of yet another item.

## Model & Data Structure
Initially, a parametric model with nonlinear characteristics was utilized as it provides the ability to measure the degree to which each modeled component manifests within the dataset. However, this can be readily expanded to a model-free or deep learning methodology. To support the user the [Fisher information](https://en.wikipedia.org/wiki/Fisher_information), which is a way of measuring the amount if information the data contains about an unknown parameter $$ \theta $$ corresponding to the choosen model. The process is fully automated for the example of a parametric multi-rotor model, for which the collectied flight data that sufficiently exposes the linear and angular dynamics of the vehicle is relatively simpel. But due to the modular approach in the parametric model the pipeline can easaliy be adjusted to a custom airframe structure. 

The effectiveness of the proposed framework was investigated on various UAVs, including multirotors and vertical take-off and landing (VTOL) UAVs. Whilst the results were promising, it also became evident throughout the course of my research that an organized methodology for gathering data is paramount to the attainment of a comprehensively generalizable model that faithfully captures the underlying physical phenomena. Especially for fixed-wing and vertical take-off and landing (VTOL) UAVs pose a significant challenge due to their exceedingly nonlinear and unstable behavior near the stall, necessitating the development of specialized flight maneuvers to explore the dynamics beyond their nominal operating point.



