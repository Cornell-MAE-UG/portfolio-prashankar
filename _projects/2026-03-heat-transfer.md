---
layout: project
title: Heat Transfer Derivation
description: Derivation of the governing equation for heat conduction in a rod 
technologies: [LaTeX]
image: /assets/images/mae3240_cover.jpg
hidden: false
---

The governing equations that describe physical quantities are fundamental to characterizing the essential behavior.
In this problem in MAE 3240 (Heat Transfer), we are tasked with deriving the governing equation in terms of temperature, $T$, for a differential element in a thin rod. 
The insight in a problem like this is not in the final expression itself but in the process. 
The real world is endlessly complex. 
The assumptions we make in deriving these expressions are key in interpreting the results we obtain from solving these governing equations, either analytically or, more often than not, numerically. 
As an engineer, it is vital that one understands how to derive and interpret governing equations because as we analyze real-world systems, it is vital to have an accurate equation governing the system's behavior. 
As an engineer interested in numerical methods, including for thermo-fluidic applications such as hypersonic flight, both the derivation of the governing equations and their discretization is vital in evaluating the results. 
For example, it is important to note the effect of diffusivity in the governing equation as diffusivity, or the lack thereof, significantly affects the numerical accuracy of the resulting simulation, namely via the stability, referred to as the CFL condition.     

The derivation can be downloaded [at this link]({{ "/assets/reports/2026-03-10-mae3240-homework-report.pdf" | relative_url }}) in PDF format.
The derivation is also included below. 

---

GIVEN: A thin rod of dimensions: $R, L$; in an environment with properties: $T_{\infty}, h$; it has a volumetric heat generation rate: $\dot{q}$; the Dirichlet boundary condition is $T(x=0)=T_{1}$ for all $t$; the initial condition is $T(t=0)=T_{i}$ for all $x$. 

FIND: (a) For a differential cylinder, the energy balance and express each term as a function of $T$; (b) Derive the governing equation; (c) Express boundary conditions and initial conditions

SCHEMATIC:

<div style="text-align: center;">
  <img src="{{ '/assets/images/mae3240_schematic.png' | relative_url }}" 
       alt="Schematic of thin rod" 
       style="width: 300px; height: auto; border-radius: 8px;">
</div>

ASSUMPTIONS: Very long rod, negligible thermal radiation, uniform radial temperature, i.e., $T = f(x,t)$, constant thermal and mechanical properties $k, \rho$, and $c_{p}$.

ANALYSIS:
Part (a): The energy balance for a control volume is:

$$\begin{gather*}
\dot{E}_{in}-\dot{E}_{out}+\dot{E}_{g}=\dot{E}_{st} \\
\dot{E}_{in}-(\dot{E}_{out,1}+\dot{E}_{out,2})+\dot{E}_{g}=\dot{E}_{st}
\end{gather*}$$

Let $\Delta v\equiv A {\mathrm{d} x}$ where $A=\pi R^{2}$ and ${\mathrm{~d} x}$ is the length of the differential control volume. 
Each term is:

$$\begin{align*}
\dot{E}_{in} &= q_{cond} = \boxed{-kA \frac{\partial T}{\partial x}} \\
\dot{E}_{out,1} &= q_{cond} = -kA\frac{\partial T}{\partial x} +\frac{\partial }{\partial x} \left( -kA\frac{\partial T}{\partial x}  \right){\mathrm{d} x}  = \boxed{-kA\left( \frac{\partial T}{\partial x} +\frac{\partial ^{2}T}{\partial x^{2}} {\mathrm{d} x}   \right)}  \\
\dot{E}_{out,2} &= q_{conv} = hP{\mathrm{d} x} (T_{s}-T_{\infty}) = \boxed{hP{\mathrm{d} x} (T-T_{\infty})} \\
\dot{E}_{g} &= \dot{q}\Delta v = \boxed{\dot{q}A{\mathrm{~d} x}  } \\
\dot{E}_{st} &= \rho c_{p} \frac{\partial T}{\partial t} \Delta v = \boxed{\rho c_{p}\frac{\partial T}{\partial t} A{\mathrm{d} x} }
\end{align*}$$

Part (b): Substitute the individual terms into the energy balance and simplify:

$$\begin{gather*}
\dot{E}_{in}-\dot{E}_{out,1}-\dot{E}_{out,2}+\dot{E}_{g}=\dot{E}_{st} \\
\cancel{ -kA \frac{\partial T}{\partial x} } - \left( -kA\left( \cancel{ \frac{\partial T}{\partial x} } +\frac{\partial ^{2}T}{\partial x^{2}} {\mathrm{d} x}   \right) \right) - (hP{\mathrm{d} x} (T-T_{\infty})) + (\dot{q}A{\mathrm{d} x} )  = \rho c_{p} \frac{\partial T}{\partial t} A{\mathrm{d} x}  \\
k\frac{\partial ^{2}T}{\partial x^{2}}\cancel{ \Delta v } - hP{\mathrm{d} x} (T-T_{\infty}) + \dot{q} \cancel{ \Delta v } = \rho c_{p}\frac{\partial T}{\partial t}  \cancel{ \Delta v } \\
k\frac{\partial ^{2}T}{\partial x^{2}} - \frac{hP{\mathrm{d} x}}{\Delta v } (T-T_{\infty}) + \dot{q} = \rho c_{p}\frac{\partial T}{\partial t}  \\
\frac{hP{\mathrm{d} x}}{\Delta v} = \frac{h\cdot 2 \cancel{ \pi } \cancel{ R }\cdot\cancel{ {\mathrm{d} x} }}{\cancel{ \pi } R^{\cancel{ 2 }} \cancel{ {\mathrm{d} x} } }=  \frac{2h}{R}  \\
\boxed{k\frac{\partial ^{2}T}{\partial x^{2}} - \frac{2h}{R}(T-T_{\infty})+\dot{q}=\rho c_{p}\frac{\partial T}{\partial t} }
\end{gather*}$$

Part (c): We have a Dirichlet boundary condition at $x=0$ and a Neumann boundary condition at $x=L$:

$$\begin{align*}
&\boxed{T(x=0,t)=T_{1}} \\
&\text{at left end: } q''_{conv}=q''_{cond} \implies -k\frac{\partial T}{\partial x} =h(T(x=L,t)-T_{\infty}) \implies \boxed{ \left. \frac{\partial T}{\partial x} \right|_{x=L} = -\frac{h}{k}(T(L,t) - T_{\infty})}
\end{align*}$$

The initial boundary condition can be expressed as $\boxed{T(x, t=0)=T_{i}}$
