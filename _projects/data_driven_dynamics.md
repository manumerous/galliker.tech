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
# accent_color: '#4fb1ba'
# accent_image:
#   background: '#193747'
# theme_color: '#193747'
sitemap: false
---

A good model of the dynamics of an unmanned aerial vehicle (UAV) is usefull for many applications including simulation, design analysis and controls. However, obtaining such models through conventional techniques 
is typically time intensive and requires additional infrastructure like wind tunnels or elaborate additional sensors. 

In contrast to this the data-driven dynamics modelling pipeline provides a framework to obtain a dynamics model by directly analyzing the flight data provided by the by default on the vehicle installed sensors. 
The dynamics models are obtained by minimizing a cost function of a parametric model for the given data. The developed framework, which I started as a semester project at ETH,
was demonstrated with several types of different UAV models, including multirotors, fixed-wing aircraft and vertical take-off and landing (VTOL) UAVs. 

The pipeline was then published as an open source project and presented at the PX4 dev summit. It provides functionalities to read and select data from the ULog file format, estimate the dynamics model and integrate it into the PX4 Gazebo flight simulator. The process is fully automated for a parametric multi rotor model and can, due to the modular approach, be extended with additional air frames and model structures in the future.