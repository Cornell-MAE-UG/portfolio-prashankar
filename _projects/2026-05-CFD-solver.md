---
layout: project
title: CFD Solver
description: Computational fluid dynamics (CFD) solver in Python using finite difference method for incompressible lid-driven cavity problem 
technologies: [Python, CFD, LaTeX]
image: /assets/images/mae4100_cover.png
imagealt: Horizontal velocity contours for 2D incompressible flow simulation in steady-state.  
hidden: false
---

This project covers the implementation of a finite-difference method (FDM)-based incompressible flow computational fluid dynamics (CFD) solver for the lid-driven cavity problem in Python. 
This is a classic problem in fluid mechanics that is described by the two-dimensional Navier-Stokes equations; the relevant quantities are the pressure, $p$, the horizontal velocity, $u$, and the vertical velocity, $v$.

$$\begin{align*}
\rho \frac{\partial u}{\partial x}+\rho \frac{\partial v}{\partial y} & = 0 \\
\rho \frac{\partial u}{\partial t}+\rho u \frac{\partial u}{\partial x}+\rho v \frac{\partial u}{\partial y}+\frac{\partial p}{\partial x} & =\mu \frac{\partial^2 u}{\partial x^2}+\mu \frac{\partial^2 u}{\partial y^2} \\
\rho \frac{\partial v}{\partial t}+\rho u \frac{\partial v}{\partial x}+\rho v \frac{\partial v}{\partial y}+\frac{\partial p}{\partial y} & =\mu \frac{\partial^2 v}{\partial x^2}+\mu \frac{\partial^2 v}{\partial y^2}
\end{align*}
$$

This project will primarily focus on density-based solvers, solving the equations with time derivative preconditioning and an artificial viscosity term to ensure numerical stability.

An initial baseline case is established with the following configurations:
- Reynolds Number: The initial simulation is run at a Reynolds number ($\mathrm{Re}$) of 100.
- Domain Dimensions: The geometry is a square cavity with a characteristic length $(L)$ of 5 cm, meaning the domain spans from 0 to 5 cm in both the $x$ and $y$ directions.
- Fluid Properties: The fluid is assumed to have a constant density $(\rho)$ of $1.0 \mathrm{~kg} / \mathrm{m}^3$.
- Boundary Conditions: The top wall (the lid) moves horizontally with a velocity ( $U_{\text {lid }}$ ) of $1.0 \mathrm{~m} / \mathrm{s}$, while the remaining three walls are stationary no-slip boundaries.
- Mesh Resolution: The baseline simulation utilizes a coarse spatial mesh of $65 \times 65$ nodes.
- Pressure Rescaling: The solver enforces a specific reference pressure of $p_{\text {ref }}=0.8013338444662 \mathrm{~Pa}$ exactly at the center of the cavity.

The project then delves into the following sections:
1. **Theory:** The theory behind the CFD solver, namely, the governing equations, boundary conditions, discretization, stability methods, namely artificial compressibility and artificial viscosity, and the iterative techniques used to march the system to a steady-state. 
2. **Iterative convergence:** Criteria for convergence to the steady-state and comparison of the convergence for serial vs vectorized code and the different iterative solver algorithms. 
3.  **Code verification:** Code verification by comparing the serial vs vectorized implementations and using the method of manufactured solutions (MMS) to compute the observed order of accuracy and verify its consistency with the scheme's theoretical order of accuracy. 
4.  **Flow analysis:** Studying the effects of changing the flow characteristics from Re = 10 to Re = 1000 flows, comparing them to each other and for consistency with fluid mechanical principles. 
5.  **Parameter study:** Studying the effects of changing three parameters in the simulation on the stability, convergence, and computational cost: the artificial viscosity parameter, $C^{(4)}$, the time preconditioning parameter, $\kappa$, and the number of nodes, $N$. 
6.  **Geometric study:** Studying the effect of the cavity geometry on the flow results and the $p$, $u$, and $v$ contours.
7.  **Literature comparison:** Comparing the results of this CFD solver with results in literature, namely Ghia et al. (1982) and Shankar & Deshpande (2000). 

The **key results and insights** from this project are:
- **Instability Mitigation:** Demonstrates how the artificial viscosity term, containing a fourth-derivative of pressure, acts as a high-frequency spatial filter, successfully suppressing odd-even pressure decoupling, i.e., checkerboard effects. 
- **Hyperbolic Restructuring:** Utilizes time-derivative preconditioning, i.e., artificial compressibility, to change the mathematical behavior of the incompressible system to hyperbolic in pseudo-time, enabling efficient explicit time-marching methods towards the steady-state solution. 
- **Method of Manufactured Solutions:** Verifies the solver's consistency with the theoretical 2nd-order of accuracy in space. 
- **Literature Comparison:** The results of this solver show high alignment with some literature and only partial alignment with others. 

The full report can be viewed and downloaded [at this link]({{ "/assets/reports/2026-05-15-mae4100-project-2-report.pdf" | relative_url }}) in PDF format.
See below for select figures from the report. 

<div style="text-align: center;">
  <img src="{{ '/assets/images/mae4100_figure_4-1_4-2.png' | relative_url }}" 
       alt="Contours of p, u, and v" 
       style="width: 300px; height: auto; border-radius: 8px;">
</div>

<div style="text-align: center;">
  <img src="{{ '/assets/images/mae4100_figure_3-2.png' | relative_url }}" 
       alt="Convergence of observed order of accuracy" 
       style="width: 300px; height: auto; border-radius: 8px;">
</div>

<div style="text-align: center;">
  <img src="{{ '/assets/images/mae4100_figure_7-1.png' | relative_url }}" 
       alt="Comparison of simulation centerline profiles with literature" 
       style="width: 300px; height: auto; border-radius: 8px;">
</div>

