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

## Explicit Euler

The explicit Euler method, also known as Forward Euler, is the simplest of the ODE solvers. Since it uses only a single first order information of the function at the beginning og the step the resulting local error is of magnitute $O(n^2)$. It is generally cpu time efficient, but not very accurate and prone to overshooting and subsequentailly becoming unstable for too large step sizes. 

The explicit Euler method is given by the following equation:

$$ x_{n+1} = x_n + \Delta t \ f(x_n, t) $$


<a href="https://github.com/manumerous/lynx-ode" class="btn btn-sm btn-primary mt1" target="_blank">
        Code
</a>

## Implicit Euler

