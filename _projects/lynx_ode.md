---
layout: project
title: 'Lynx ODE'
caption: A versatile and light-weight headers only library for ODE solvers in C++
# description: >
#   While Hydejack is built for personal sites, it's versatility allows it to be used a product page as well.
date: '11-06-2023'
image: 
  path: /assets/img/projects/lynx_ode/lorenz_attractor.png
  srcset: 
    1920w: /assets/img/projects/lynx_ode/lorenz_attractor.png
links:
  - title: Link
    url: https://github.com/manumerous/lynx-ode
accent_color: '#136EAE'
# accent_image: /assets/img/projects/bipedal_locomotion_mpc/amber-min.jpg
background: '#136EAE'
theme_color: '#136EAE'
sitemap: false
---

A versatile and light weight like a lynx! This headers only C++ library containing Ordinary Differentail Equations (ODE) solvers that can be used to simulate dynamical systems.

The following methods are currently included:

- Explicit Euler (also known as Forward Euler)
- Implicit Euler (also known as Euler Backward)
- 2nd Order Runge-Kutta
- 4th Order Runge-Kutta

## ODE solvers

An ODE (Ordinary Differential Equation) solver is a computational algorithm used to simulate dynamical systems to model a wide range of time varying phenomena in physics, engineering, biology and economics among others. The dynamical system is typically described by a set of states containing information about the internal conditions of the system. How the system evolves over time, as characterized by the rate of change of it's states, is described as a function of time and the current state itself, resulting in an ordinary differential equation.

$$ \dot{x} = f(x, t) $$

Given an initial state $x_0$ at time $t_0$, the ODE solver is then used to forward integrate the system over time, resulting in a time series of states $x(t)$.

The following ODE solvers are currently included in the library:

### Explicit Euler

The explicit Euler method, also known as Forward Euler, only uses a single evaluation of the system dynamics at the current state and time. This gives the algorithm first order information of the system dynamics for each time step resulting in a local error is of magnitute $O(n^2)$. It is generally cpu time efficient, but not very accurate and prone to overshooting and subsequentailly becoming unstable for too large step sizes. 

The explicit Euler method is defined as follows:

$$ x_{n+1} = x_n + \Delta t \ f(x_n, t_n) $$

### Implicit Euler

Instead of evaluating the first order information at the beginning of the step the implicit euler or euler backwards method evaluates the system dynamics at the end of each time step to reduce the risk of numeric instabilities at the cost of additional complexity. Also this first order method has a local error of magnitute $O(n^2)$

The implicit Euler Method is defined as follows: 

$$ x_{n+1} = x_n + \Delta t \ f(x_{n+1}, t_{n+1}) $$


<a href="https://github.com/manumerous/lynx-ode" class="btn btn-sm btn-primary mt1" target="_blank">
        Code
</a>

## Implicit Euler

