## Legged Robot Dynamics
The dynamics of a legged robot are typically described as a *Nonlinear Control-Affine Hybrid System*. 

**Nonlinear Control-Affine System:**
A dynamic system is a process or system wherein the inherent configuration, known as the state of the system, changes over time. Such a system can be mathematically described through an ordinary differential equation. In case of a *Nonlinear Control-Affine System*, as is the case for many physical systems with appropriate choice of input $$\mathbf u$$, the change over time of state vector $$\mathbf x$$ is described as a nonlinear function of the state itself and a linear function of the input vector  

$$
 \frac{d}{dt} \bm x = \dot{\bm x} = f(\bm x) + g(\bm x) \bm u
$$

**Hybrid System:**
A hybrid system is a system where the inherit dynamics exhibit both continuous characeristics and discrete jumps. In chase of a legged robot the discrete dynamics occure when the system establishes or breaks contact ( e.g. foot impact).


<div style="width: 80%; margin: 5%;">
  <p align="center"><img src="/assets/img/projects/bipedal_locomotion_mpc/hybrid_dynamics_web.png"></p>
  <p align="center"><em>Fig.1 - Continuous and discrete dynamics of a legged robot.</em></p>
</div>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      extensions: ["AMSmath.js"]
    }
  });
</script>
<script async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML"></script>

### System Dynamics

for the set of generalized coordinates containing 


$$
 \mathbf{D}(\bm q)\ddot{\bm q}+\bm{h}(\bm q, \dot{\bm{q}}) = \mathbf{B}(\bm q)\bm{\tau} +  \mathbf{J}_{c}(\bm q)\bm{\lambda}
$$

$$
    \bm{J}_c(\q) \ddot{\q} + \dot{\bm{J}}_c(\q,\dot{\q}) \dot{\q} &= \bm 0
$$