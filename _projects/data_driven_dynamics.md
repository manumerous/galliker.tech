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
In this research project, I aimed to address this challeng by proposing a data-driven dynamics modelling pipeline that uses the [PX4 unified flight log (ULog)](https://docs.px4.io/main/en/dev_log/ulog_file_format.html) format. The primary objective was to establish a framework for obtaining a dynamics model solely by minimizing the prediciton error of the model with respect to the flight data collected by the by default on the vehicle installed sensors. The effectiveness of the proposed framework was investigated on various UAVs, including multirotors and vertical take-off and landing (VTOL) UAVs. Specifically, for the example of multirotors, the pipeline automates the joint estimation of the UAV's dynamics model and the quality of the fit and integrates the former into the [PX4 Gazebo flight simulator](https://github.com/PX4/PX4-SITL_gazebo-classic).The data-driven-dynamics pipeline is published as an [open source project on Github](https://github.com/ethz-asl/data-driven-dynamics) and presented at the [Linux Foundation PX4 Developer Summit 2021](https://events.linuxfoundation.org/archive/2021/px4-developer-summit/).

## Overview of the Pipeline
The data-driven dynamics pipeline is implemented in python and consists of the following main modules: 

<p align = "center"><img src = "/assets/img/projects/data_driven_dynamics/PipelineDiagramm_bar.png"></p><p align = "center">
<em>Fig.1 - Main building blocks of the data-driven-dynamics pipeline.</em>
</p>

- **Data Processing:** Responsible to load and preprocess the data used to estimate the dynamics model. It contains functionalities to filter, resample and normalize the data.
- **Data Selection** Optionally the user has the ability to visualize the data and additional  step to visually select a suportion of the data that is best suited to estimate the dynamics model. 
- **Model Definition** Contains the model structure used to predict the dynamics. A selection of parametric models pertaining to fundamental components, such as rotors and wings, is available and can be utilized to construct a model tailored airframe. The framework is not limited to a specific methodology and can be extended to incorporate model-free or deep learning approaches.
- **Optimization Framework** Interfaces the choosen model and a cost function with an optimization framework. Currently supported optimization frameworks include cvxpy and the sklearn linear regressor. 
- **Dynamics Model Output** The output of the parametric model is automatically saved onto a YAML file that is then used to integrate the estimated dynamics into Gazeboo via a C++ plugin.

## Dynamics model for UAVs

Unmanned Aerial Vehicles (UAVs) can be modeled as dynamic systems, and their behavior can be described using mathematical models that capture the underlying physics. The single rigid body dynamics (SRBD) model assumes that the UAV is a rigid body that has six degrees of freedom (3 linear and 3 rotational), and it can be modeled using the following equations:

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      extensions: ["AMSmath.js"]
    }
  });
</script>
<script async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML"></script>

$$
\dot{\bm x} = \frac{d}{dt}
\left(\begin{array}{c}
_{\mathcal{I}}{\mathbf{r}}    \\
 {\bm{\xi}}_{\mathcal{I}\mathcal{B}}  \\
{_{\mathcal{B}}}{\mathbf{v}}  \\
{_{\mathcal{B}}}{\bm{\omega}}
\end{array}\right) = 
\left(\begin{array}{c}
{\mathbf{R}}_{\mathcal{I}\mathcal{B}} \cdot {_{\mathcal{B}}}\mathbf{v}    \\
\bm{\chi}^{-1} \bm{\omega}  \\
\frac{1}{m} {\mathbf{R}}_{\mathcal{I}\mathcal{B}} \cdot { _{\mathcal{B}}}\mathbf{F} + _{\mathcal{I}}\mathbf{g} \\
{_{\mathcal{B}}}\mathbf{I}^{-1} ({_{\mathcal{B}}}\mathbf{M} - {_{\mathcal{B}}}\bm{\omega}^{} \times {_{\mathcal{B}}}\mathbf{I} \cdot {_{\mathcal{B}}}\bm{\omega})
\end{array}\right)  \tag{1}
$$

where the state vector $$\bm x \in \in \mathbb{R}^13$$  contains the position vector $$\mathbf{r} \in \mathbb{R}^3$$, the unit quaternion $$\boldsymbol{\xi}_{\mathcal{I}\mathcal{B}} \in \mathbb{S}^4$$ and the linear and anular velocity vectors $$\mathbf{v} \in \mathbb{R}^3$$ and $$\mathbf{\omega} \in \mathbb{R}^3$$ respectively. $${\mathbf{R}}_{\mathcal{I}\mathcal{B}} \in \mathbb{R}^{3 \times 3}$$ is the rotation matrix representing the rotation from body frame $$\mathcal{B}$$ into inertial frame $$\mathcal{I}$$, $$\mathbf{F} \in \mathbb{R}^3$$ is the net aerodynamic force acting on the body, $$\mathbf{g} \in \mathbb{R}^3$$ is the gravitational force, $$\mathbf{M} \in \mathbb{R}^3$$ is the net moments acting on the body, $$m \in \mathbb{R}$$ is the mass of the body, and $$\mathbf{I} \in \mathbb{R}^{3 \times 3}$$ is the inertia tensor of the body.

<div style="width: 80%; margin: auto;">
  <p align="center"><img src="/assets/img/projects/data_driven_dynamics/dynamics_model2.png"></p>
  <p align="center"><em>Fig.1 - Forces and moments apllying on fixed-wing UAV (by Thomas Stastny).</em></p>
</div>

As can be seen in equation $$(1)$$ the main unknowns that need to be determined are the aerodynamic forces (e.g. thrust, lift, drag) and moments (roll, pitch and yaw) and inertia tensor. Alternatively to estimating those separately it is also possible to directly estimate the the linear and angular acceleration, which practically lumps the estimation of the moments and inertia tensor together.  

## Model Structure & Data Quality
Throughout the course of my research, I came to realize that the primary obstacle in estimating UAV dynamics lies not in the actual modeling of the dynamics but rather in obtaining and verifying an appropriate dataset. For accurate estimation of a UAV's dynamics, the dataset must capture all the relevant physical effects independently and adequately covers of the state input-space of the system. Otherwise, significant discrepancies in the estimated dynamics model will be observed when evaluated beyond the distribution of the training data. Furthermore, external effects such as wind conditions 

Therefore, even for a relatively uncomplicated platform such as a multirotor, an organized methodology for gathering and validating data is paramount to the attainment of a comprehensively generalizable model that faithfully captures the underlying physical phenomena. 
The challenge of selecting an appropriate dataset becomes even greater for fixed-wing and vertical take-off and landing (VTOL) UAVs, as they exhibit highly nonlinear behavior and instability near the stall. This necessitates the development of specialized flight maneuvers that explore the dynamics beyond their nominal operating point and potentially outside if the vehicles narrow stability range (e.g. post stall regime). 

### Parametric Model
To adress the challenges named above a hand-crafted parametric model has several advantages. This model choice provides a high degree of control over its fidelity, making the collection of a compatible dataset significantly easier. Moreover, it allowes us to quantitatively estimate how much information on a certain parameter is present in the data set. For a model that is linear with respect to its parameters (but potentially nonlinear with repect to its state $$\bm x$$ or input $$u$$) this can easily be computed through a significance test and correlation matrix of the parameters w.r.t. the data. For a nonlinear parametric model a more suffisticated approach like the Fisher information can be used. 

### Assessment of Data Quality via Fisher Information
Through the computation of [Fisher information](https://arxiv.org/pdf/1705.01064.pdf) an estimate of how much information data provides for estimating a parameter $$\theta$$. This is achieved via a sensitivity analysis w.r.t $$\theta$$ of the logarithmic likelyhood to observe measurement X given parameter value.

$$
I(\theta) = -\mathbb{E}\left[\frac{\partial^2}{\partial \theta^2} \log f(X | \theta)\right] \tag{2} 
$$

where $$I(\theta)$$ is the Fisher information with respect to the parameter $$\theta$$, $$ f(X | \theta) $$ is the probability density function of observing the random variable $X$ given the parameter $$\theta$$, and $$\mathbb{E}$$ denotes the expected value operator.
<!-- The Fisher information matrix, which is defined as the second partial derivatives of the log-likelihood function of observing the measurement given parameter $$\theta$$, provides information on the precision of estimated parameters and the correlation between parameters. -->

<!-- It allowes tight control over the fidelity of the modelwhich drasticall yfascilitas the job of collecting a matching dataset. Additionally, through the computation of the [Fisher information](https://arxiv.org/pdf/1705.01064.pdf) enables quantification of the extent to which each modeled component is evident in the dataset. The Fisher information matrix is a matrix of second partial derivatives of the log-likelihood function with respect to the parameters. The diagonal elements of this matrix indicate the precision of the estimated parameters, while the off-diagonal elements indicate the extent to which the parameters are correlated.



However, this can be readily expanded to a model-free or deep learning methodology. -->

### Video Presentation at the PX4 Developer Summit 2021

<div class="videoWrapper">
<iframe src="https://www.youtube.com/watch?v=kAsfptZU4uk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>



