---
layout: project
title: 'Nonlinear MPC for Bipedal Locomotion'
caption: Online gait generation using whole-body dynaics.
# description: >
#   While Hydejack is built for personal sites, it's versatility allows it to be used a product page as well.
date: '05-03-2022'
image: 
  path: /assets/img/projects/bipedal_locomotion_mpc/amber-min.jpg
  srcset: 
    1920w: /assets/img/projects/bipedal_locomotion_mpc/amber-min.jpg
links:
  - title: Link
    url: https://hydejack.com/
accent_color: '#383737'
accent_image: /assets/img/projects/bipedal_locomotion_mpc/amber-min.jpg
background: '#383737'
theme_color: '#383737'
sitemap: false
---

In this project I explored and developed 
The ability to generate dynamic bipedal walking in real-time for bipedal robots with input constraints and underactua-
tion has the potential to enable locomotion in dynamic, complex and unstructured environments. Yet, the high-dimensional nature of bipedal robots has limited the use of full-order rigid body dynamics to gaits which are synthesized offline and then
tracked online. As part of my master thesis I explored, developed and sucessfully tested an online nonlinear model predictive control approach that leverages the full-order dynamics to realize diverse walking behaviors. Additionally, building up on prior work of [Noel Csomay-Shanklin](https://noelc-s.github.io/website/) we coupled this approach with offline synthesized gaits to enable a shorter prediction horizon and rapid online re-planning. 

The following discussion is meant to give a quick overview of the methodology employed in the paper: *Planar Bipedal Locomotion with Nonlinear Model Predictive Control: Online Gait Generation using Whole-Body Dynamics*.

<a href="https://arxiv.org/pdf/2203.07429.pdf" class="btn btn-sm btn-primary mt1" target="_blank">
        <small class="icon-file-pdf"></small>
        Paper
</a>
<a href="/assets/documents/projects/bipedal_locomotion_mpc/Humanoids_TO_MPC_Workshop_Poster.pdf" class="btn btn-sm btn-primary mt1" target="_blank">
        <small class="icon-file-pdf"></small>
        Poster
</a>
<a href="/assets/documents/projects/bipedal_locomotion_mpc/Paper_Presentation_Humanoids_short.pdf" class="btn btn-sm btn-primary mt1" target="_blank">
        <small class="icon-file-pdf"></small>
        Presentation Slides
</a>
<a href="https://www.youtube.com/watch?v=3g8ZNsCWdOA" class="btn btn-sm btn-primary mt1" target="_blank">
        Experimental Results
</a>
<a href="https://www.youtube.com/watch?v=zMjEMkBBRbg&t=19s" class="btn btn-sm btn-primary mt1" target="_blank">
        Presentation - Humanoids 2022
</a>

<a href="https://mediaspace.wisc.edu/media/DW22_Csomay-Shanklin%2C+Noel+-+June+15th+2022%2C+7A39A39+pm/1_das1yjvq" class="btn btn-sm btn-primary mt1" target="_blank">
        Presentation - Dynamics Walking 2022 
</a>

## Reparametriced Whole-Body MPC
Due to the computational cost of optimizing a policy online using MPC most approaches so far have relied on simplified (Linear Inverted Pendulum, Spring-Loaded Inverted Pendulum, Single Rigid Body, ect.) or reduced models (Center of Mass Dynamics). Although these simplified/reduced models can achieve impressive performance for bipedal locomotion they also have their downsides. In particular, their capability to leverage the true nonlinear dynamics and underactuation is limited and they can not take dynamics constraints such as actuator torque limits into account. Furthermore, since they produce a simplified policy they need to be combined with a Whoole-Body Controller to control the robot in torque mode. 

Therefore, I started to explore the possibility to extend existing MPC frameworks by planning directly over the Whole-Body Dynamics. For this I proposed the use of a reparametrication of the whole-body dynamics that optimized directly over the joint accelerations $$\ddot{\bm q_j}$$. 

The MPC system dynamics are defined as follows:

<div style="width: 80%; margin: 5%;">
  <p align="center"><img src="/assets/img/projects/bipedal_locomotion_mpc/reparametriced_wb_mpc.png"></p>
</div>

Where $$\bm q$$, $$\ddot{\bm q_j}$$, $$\ddot{\bm q_j}$$ and $$\bm \lambda$$ are the generalized coordinates, generalized velocities, generalized joint accelerations and external contact forces. As can be seen, this reparametrication focusses most of the computational complexity on the underactuated dynamics. Furthermore by excluding the *Inverse Dynamics* from the model prediction step the computation of the generalized mass matrix $$\mathbf{D(\bm q)}$$, the nonlinear effects $$\bm{h}(\bm q, \dot{\bm{q}})$$ and the contact Jacobian $$\mathbf{J}_{c}$$ can be limited to the first 6 components that influence the dynamics of the base link. Furthermore, due to the partially (block) diagonal nature of the generalized mass matrix corresponding to the base $$\mathbf{D_{bb}}(\bm q) \in \mathbb{R}^{6 \times 6}$$ the effectively needed to compute invers in only of dimensionality $$\mathbb{R}^{3 \times 3}$$

Despite those computational benefits, there is actually no loss of information and the planned joint torques can simply be recovered through inverse dynamics for every point along the planning horizon:

$$
  \bm{\tau} = \mathbf{D}(\bm q)\ddot{\bm q}+\bm{h}(\bm q, \dot{\bm{q}}) - \mathbf{J}_{c}(\bm q)\bm{\lambda}
$$

This way is is possible to add for example a torque limit to the optimization. By doing this as a part of the "sensitivity analysis" of the MPC problem, instead of in a single shooting model prediction step (as done for example in Differential dynamic programming), this computation can be parallelized.

The proposed MPC is then combined with a low level controller that recovers the planned torques and accounts for model missmath through an additional feedback term. 


<div style="width: 100%; margin-top: 40px;">
  <p align="center"><img src="/assets/img/projects/bipedal_locomotion_mpc/MPCPipeline_v2_web.jpg"></p>
</div>



## Combination with offline generated Hybrid Zero Dynamics Gaits

I am still working on documenting this part. 


## Experimental Results

### Paper Submission Results Video
The video is rather rushed due to the time limit of the conference submission, but it highlights the most important experimental results.  

<div class="videoWrapper">
<iframe src="https://www.youtube.com/embed/3g8ZNsCWdOA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>



