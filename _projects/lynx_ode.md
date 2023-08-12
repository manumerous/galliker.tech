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

This headers only C++ library contains a range of Ordinary Differential Equations (ODE) solvers that can be used to simulate dynamical systems.

## ODE Solvers

An ODE (Ordinary Differential Equation) solver is a computational algorithm used to simulate dynamical systems to model a wide range of time varying phenomena in physics, engineering, biology and economics among others. The dynamical system is typically described by a set of states containing information about the internal conditions of the system. How the system evolves over time, as characterized by the rate of change of it's states, is described as a function of time and the current state itself, resulting in an ordinary differential equation.

$$ \dot{\bm x} = \bm f(\bm x, t) $$

Given an initial state $$\bm x_0$$ at time $$t_0$$, the ODE solver is then used to forward integrate the system over time, resulting in a time series of states $$\bm x(t)$$. This ODE describing the dynamical system is also referred to as the system flow map. 

## Included ODE Solvers

The following methods are currently included:

- Explicit Euler (also known as Forward Euler)
- Implicit Euler (also known as Euler Backward)
- 2nd Order Runge-Kutta
- 4th Order Runge-Kutta

### Explicit Euler

The explicit Euler method, also known as Forward Euler, only uses a single evaluation of the system flow map at the current state and time. This gives the algorithm first order information of the system dynamics for each time step resulting in a local error is of magnitude $$ O( \Delta t^2 ) $$. It is generally cpu time efficient, but not very accurate and prone to overshooting and sub-sequentially becoming unstable for too large step sizes. 

The explicit Euler method is defined as follows:

$$\bm  x_{n+1} =\bm x_n + \Delta t \ \bm f(\bm x_n, t_n) $$

### Implicit Euler

Instead of evaluating the system flow map at the beginning of the step the implicit euler or euler backwards method evaluates at the end of each time step. This reduces the risk of numeric instabilities at the cost of additional complexity. Also this first order method has a local error of magnitude $$O(\Delta t^2)$$

The implicit Euler Method is defined as follows: 

$$\bm x_{n+1} = \bm x_n + \Delta t \ \bm f(\bm x_{n+1}, t_{n+1}) $$

### Runge-Kutta Method

In contrast to the discussed first order methods (which can be seen as first order Runge-Kutta methods) the higher order Runge-Kutta methods evaluate the system flow map multiple times within one time step. This way it is possible to include higher order information of the system flow map into a single prediction step. The local error of a kth order Runge-Kutta method is of order $$O(\Delta t^{k+1})$$. 

#### 2nd Order Runge-Kutta
the 2nd order Runge-Kutta solver first evaluated the direction of a single euler forward step and then evaluates the system flow map at a half step in that direction. 

$$
\begin{align*}
\bm k_1 & = \Delta t \  \bm f(\bm x_n, t_n) \\

\bm k_2 & = \Delta t \ \bm f\left(\bm x_n + \frac{\bm k_1}{2}, t_n + \frac{\Delta t}{2}\right) \\

\bm x_{n+1} & = \bm x_n + \bm k_2
\end{align*}
$$

#### 4th Order Runge Kutta
The 4th Order Runge-Kutta solver evaluates the system flow map at 4 distinctive points, with consecutive evaluations building up on the previous one, and then takes a weighted average over the 4 direction to account for the curvature of the real system dynamics. 

$$
\begin{align*}
\bm{k}_1 & = \Delta t \bm f(t_n, \bm{x}_n) \\
\bm{k}_2 & = \Delta t \bm f\left(t_n + \frac{\Delta t}{2}, \bm{x}_n + \frac{\bm{k}_1}{2}\right) \\
\bm{k}_3 & = \Delta t \bm f\left(t_n + \frac{\Delta t}{2}, \bm{x}_n + \frac{\bm{k}_2}{2}\right) \\
\bm{k}_4 & = \Delta t \bm f(t_n + \Delta t, \bm{x}_n + \bm{k}_3) \\
\bm{x}_{n+1} & = \bm{x}_n + \frac{1}{6}(\bm{k}_1 + 2\bm{k}_2 + 2\bm{k}_3 + \bm{k}_4)
\end{align*}
$$


<a href="https://github.com/manumerous/lynx-ode" class="btn btn-sm btn-primary mt1" target="_blank">
        Code
</a>


