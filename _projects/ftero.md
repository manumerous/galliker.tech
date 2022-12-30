---
layout: project
title: 'Fast Prototyping for Airborne Wind Energy'
caption: At the intersection of sustanable energy and aerial robotics.
# description: >
#   At the intersection of sustanable energy and aerial robotics.
date: '01-06-2018'
image: 
  path: /assets/img/projects/ftero/AWE_title.png
  srcset: 
    1920w: /assets/img/projects/ftero/AWE_title.png
links:
  - title: Link
    url: https://structures.ethz.ch/education/bachelor/focusprojects/focus-project-awe.html
sitemap: false
---
Over the past few decades, there has been a clear trend towards the use of renewable energy sources. Energy security and sustainability are major concerns for countries around the world. Despite significant advancements in well-established renewable energy technologies such as wind and solar, there is still a need for innovative solutions that can provide large amounts of electricity at a competitive cost.
Airborne Wind Energy (AWE) represents one family of such innovative approaches.

## Airborne Wind Energy

AWE systems harness the power of wind through a unmanned aerial vehicle (UAV) consiting of a wing or kite, connected to the ground via a tether, to generate electricity. Hereby, the power can either be generated onboard, where the energy is harvested by an onboard turbine and generator and conducted to the ground through the tether, or on-ground, where the resulting aerodynamic forces are transferred through the tether to a generator on the ground.  

<p align = "center"><img src = "/assets/img/projects/ftero/power_generation_graphic.png"></p><p align = "center">
<em>Fig.1 - Onboard power generation (left). Traction and retraction phase of on-ground power generation (right).</em>
</p>


AWE systems have several potential advantages over traditional wind turbine systems, including:

- Lower cost: AWE systems are typically lighter and require fewer materials than wind turbines, making them less expensive to manufacture and install.

- Increased efficiency: AWE systems can harness winds at higher altitudes, where winds tend to be stronger and more consistent than at ground level.

- Unlocking additional wind resources: AWE systems can be deployed in a variety of locations, including deep sea offshore areas, where traditional wind turbines may not be feasible.

Despite their potential benefits, AWE systems are still in the early stages of development and have in 2022 not yet been widely deployed due to several technical and regulatory challenges, including issues related to safety and reliability. You can learn more about AWE in [R. Schmehl, "Airborne Wind Energy – An introduction to an emerging technology", 2019](http://awesco.eu/awe-explained/).

## The Focus Project ftero

During the last year of my bachelor studies at ETH Zurich I joined the focus project ftero as one of eight students where we developed, designed and prototyped a small scale AWE system and investigated various research questions related to flight controls and adaptive lightweight composite structures. Hereby we were supported and supervised by the [Autonomous Systems Lab](https://asl.ethz.ch/) of Prof. R. Siegwart and the [Composite Materials and Adaptive Structures Lab](https://structures.ethz.ch/) by Prof. P. Ermanni. 

We pursued an approach to AWE which encompasses a ground based generator powered by an fixed-wing unmanned aerial vehicle. The kinetic energy of the wind is harvested by the carbon wing in the form of lift. By flying on a spiral path, the wings pull on the tether, there­by actuating the generator, resulting in electrical power generation.

 <div class="row">
  <div class="column">
    <img src="/assets/img/projects/ftero/wing_electronics.png" alt="Wing Structure and Electronics" style="width:100%">
  </div>
  <div class="column">
    <img src="/assets/img/projects/ftero/1660642231694.jpeg" alt="Flight Test of Vertical Take-Off" style="width:100%">
  </div>
</div>
<div align = "center">
  <em >Fig.2 - Wing structure and electronics (left). Hover Flight test for vertical take-off and landing (right).</em>
</div> 

During the project had the role of team leader for software and mechatronics where I coordinated our efforts in system modeling, controls, actuation and electronics. 

### System Modelling and Controls
For the flight dynamics modelling we extended an established aerodynamic fixed-wing model, consisting of a lift drag model of our UAV obtained from CFD, by the additional tether force. The tether force was implemented as a spring damper system and added to the fixed-wing model in PX4s SITL Gazebo.   

On the controls side we used the [Px4 L1 Controller](https://docs.px4.io/main/en/flight_stack/controller_diagrams.html#fixed-wing-position-controller) to generate roll setpoints that keep the UAV on a circular path in the lateral direction. Furthermore our controller had to balance the kinetic and potential energy in order to ensure that the UAV can reach the next apex in the planned trajectory while also maximizing the power output. Here we expored several methodologies including controlling the pitch, angle of attack of the wing, tether force or adapting a [Total Energy Control System (TECS)](https://docs.px4.io/main/en/flight_stack/controller_diagrams.html#fixed-wing-position-controller) approach. The controller was implemented into the PX4 Autopilot in C++ and sucessfully tested on an easy glider platform using a STM32F469 processor.

A more thorough control approach using Nonlinear Model Predictive Control approach was explored alongside the project ftero which is published in [T. Stastny, E. Ahbe, M. Dangel, R. Siegwart. (2019). "Locally Power-optimal Nonlinear Model Predictive Control for Fixed-wing Airborne Wind Energy"](https://www.researchgate.net/publication/335856230_Locally_Power-optimal_Nonlinear_Model_Predictive_Control_for_Fixed-wing_Airborne_Wind_Energy).

### Project Video

<div class="videoWrapper">
<iframe src="https://www.youtube.com/embed/-lBixIJ9kxo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<!-- 
 To be able to meet the rising demand for renewable energy, innovative solutions are required. For this purpose, the project ftero at ETH Zurich is developing an Airborne Wind Energy System. Using an unmanned aircraft that is tethered to the ground, the system can capture wind energy and turn it into electricity with an efficiency that surpasses conventional wind turbines. The aircraft is carried by the wind like a kite, while a generator on the ground creates electricity by slowly unwinding the tether that connects the two. During nine months, the ftero team comprised of ten bachelor students went through all the steps of product development, from the idea to the finished product. -->
