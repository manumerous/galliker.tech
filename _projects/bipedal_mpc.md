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

The following discussion is meant to be a more accesible exposition of the methodology employed in the paper: *Planar Bipedal Locomotion with Nonlinear Model Predictive Control: Online Gait Generation using Whole-Body Dynamics*.

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

## Legged Robot Dynamics


![Cute Puppy](/assets/img/projects/bipedal_locomotion_mpc/hybrid_dynamics_web.png)

### Project Video

<div class="videoWrapper">
<iframe src="https://www.youtube.com/embed/3g8ZNsCWdOA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
