---
layout: default
title: Data-Driven Modelling and Control of a UAV (Safran Electronics & Defense)
permalink: /projects/uav-control/
---

[← Back to home]({{ '/' | relative_url }})

# Data-Driven Modelling and Control of a UAV 
<span class="project-tag">Industry challenge</span>
<p class="project-meta"> CentraleSupélec · Nov 2025 · one-week challenge</p>

## Problem

Safran's ground drone has a limited field of view for obstacle detection, and the proposed fix was to mount a quadrotor on a platform at the rear of the vehicle: it takes off, gathers data from above, and lands back on the platform while the vehicle moves.

The catch was that the UAV came with no technical documentation. With no physical model to start from, everything had to be recovered from data: input signals (motor torques and control commands) and output signals (accelerations), plus a Simulink model of the system. The sensors were known to be unreliable, so the measurements could not be trusted as given.

The chain to build, in one week: validate the data, justify a sampling period, identify a model, and design a control law for the three-step mission.

## Approach

**Data validation.** Screening on the minimum across output channels per time step isolated four timestamps with physically implausible values, below the mechanical limits of the system. Those samples were removed from both input and output sets, and the remaining data realigned and normalised.

**Sampling period.** The measured response reaches steady state in about 0.5 s. Applying the usual rule of a sampling period at least ten times below the dominant time constant gives 0.05 s, which held up across every model trained afterwards.

**Identification.** A first-order linear model came first as an interpretable baseline; it tracked the response but left a relative error reaching 10% over a wide range of operating conditions. Recurrent models were then trained to capture the nonlinear effects, first an LSTM and then a plain RNN. The RNN was retained: comparable accuracy, lower computational cost, and easier integration into Simulink. Test MSE settled at 0.045 per batch, in line with the final training loss.

**Control.** An output MPC was built on the RNN as its internal prediction model, predicting the system response directly from measured outputs. Prediction and control horizons at 15 steps, weights Q = 3 and R = 1, with physical limits imposed on the control inputs. A discrete Kalman filter was added to the loop to estimate the state under sensor noise and feed cleaner feedback to the controller.

Identification ran in Python with PyTorch; the trained weights were exported into Simulink, where the controller was implemented and validated against the UAV model.

## Result

The closed loop tracks the altitude reference steps, each after a short transient, with the controller staying inside the imposed input constraints and the Kalman filter suppressing the measurement noise in the feedback path.

Two defects are visible and worth naming. The drone drops briefly before converging at the start of each run, which traces back to every training sequence beginning at zero, so the model carries that bias into the controller. And a small overshoot before settling indicates the MPC and model dynamics combine into something slightly under-damped. Retraining on sequences cropped past the zero-input segment would address the first; adding integral action to the state would help the residual error.

## What I took from it

Coupling a learned model to a controller exposes model error in a way that offline metrics do not. The RNN validated cleanly against held-out data, and the steady-state error only appeared once it sat inside the MPC loop. The prediction accuracy that matters is the one measured in closed loop.

The week also made the case for keeping an interpretable baseline around. The first-order model was too coarse to control well, but having it made it obvious what the recurrent model was actually buying.
