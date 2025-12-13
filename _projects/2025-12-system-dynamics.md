---
layout: project
title: System Dynamics Analysis of T-150
description: Analysis of the yaw control of a military unmanned aerial system starting from first principles to feedback control
technologies: [MATLAB, SOLIDWORKS, Simulink, LaTeX]
image: /assets/images/mae3260_cover.png
---

In this analysis, my group studied the yaw control of the BAE/Malloy T-150 heavy-lift unmanned aerial system (UAS). Since flight dynamics are naturally nonlinear, we first linearized the equations of motion for steady, standard, flight conditions. We aimed to maximize the stability around a desired yaw angle, while maintaining constant altitude above the ground and rejecting disturbances. We studied the dynamics surrounding this system based on the inertial measurement unit (IMU), developed the relevant ODEs and thus the transfer functions, generated the block diagram for our system, and then implemented PD control. After the controller was implemented, we used Bode plot analysis in order to further understand the system behavior of different configurations of payloads. Our analysis does not consider the GPS navigation system, pitot-static system and other pressure-based instruments, and other electronic sensors.

The primary ODE that describes the control of the UAS is given by 
\[J_z \ddot{\psi} = \tau_z + \tau_d$$ where $$\psi\]
is the yaw angle and $$\tau_z$$ is the control torque. The power change to the motors is approximately given by $$\Delta P = \frac{3}{8} \omega_h \tau_z$$. The ideal feedback controller was a PD controller which retains the proportional correction and provides needed damping through the derivative term without further destabilizing the dynamics. The gain values were $$K_P = 11$$ and $$K_D = 37$$. The Bode plots showed that the UAS without the payload $$(J_z =  31\mathrm{~kg \cdot m^2} )$$ is much more agile thatn the UAS with the payload $$J_z = 69 \mathrm{~kg \cdot m^2}$$. 

[Download the final report]({{ "/assets/reports/2025-12-10-mae3260-final-report.pdf" | relative_url }}) in PDF format.