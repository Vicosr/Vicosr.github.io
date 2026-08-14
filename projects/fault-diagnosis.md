---
layout: default
title: Robot Fault Diagnosis via Sim-to-Real Domain Adaptation
permalink: /projects/fault-diagnosis/
---

[← Back to home]({{ '/' | relative_url }})

# Robot Fault Diagnosis via Sim-to-Real Domain Adaptation

<span class="project-tag">Lab project</span>
<p class="project-meta">CentraleSupélec LGI · DANN architecture and evaluation · Jan 2025 – Jun 2025</p>

## Problem

The task was to diagnose faults on a six-axis industrial robotic arm (complete actuator blockage, steady-state angular inaccuracy) from the arm's dynamic response to a command alone, with no access to internal signals such as voltage, temperature or encoder readings. This black-box setting is simple to deploy but leaves little to work with.

The harder constraint was data. Industrial arms are engineered not to fail, so labelled real fault data is scarce: the dataset held 10 real samples per class, 90 in total. Simulated faults generated from a digital twin are cheap to produce in bulk, but they do not follow the same distribution as real sensor readings. Computing the cosine similarity between each simulated trajectory and the real trajectories of its class gave a distribution centred around 0.7, with a long tail of simulations bearing little resemblance to anything real. Training on simulation and testing on hardware is therefore a domain adaptation problem, not a supervised classification problem.

The reference to beat was the client's existing MATLAB algorithm, at 86% accuracy. The client is Zhiguo Zeng, a researcher at CentraleSupélec's Industrial Engineering Laboratory working on system reliability and predictive maintenance. The brief had two parts: improve on that accuracy, and deliver a Python implementation to replace the MATLAB one.

## Approach

I built the project's main model, a Domain-Adversarial Neural Network (DANN).

The feature extractor is a 1-D convolutional stack: an initial convolution (64 filters, kernel 7) with batch normalisation and ReLU, followed by four residual blocks of increasing width (64 to 512), squeeze-and-excitation attention adapted to 1-D signals, and global average pooling for length invariance. On top of it sit two heads: a task classifier and a domain discriminator connected through a gradient reversal layer. Training the two jointly pushes the extractor toward features that are discriminative for fault classification while remaining uninformative about whether the input came from simulation or from the real arm.

Training used 2,880 simulated samples across nine fault classes. Of the real data, 30% was used for domain adaptation and the remaining 70% held out for final evaluation.

## Result

The DANN reached 87% accuracy on real robot data. The reference it was measured against, 86%, is the MATLAB solution written by the lab researcher who owns the problem and whose research field is precisely reliability and predictive maintenance, tuned by him on his own data.

Reaching that level came with a different set of constraints: the DANN sees fault labels only in simulation, and only 90 real samples exist in total. The project's second deliverable also mattered as much as the number: a modular PyTorch implementation replacing the MATLAB prototype, extensible to other equipment and to other domain adaptation techniques.

Two other architectures were evaluated alongside for comparison: an LSTM baseline, and a Graph Transformer Network, which reached 73.33% in its best configuration and was clearly limited by the size of the dataset rather than by the approach.

## What I took from it

An earlier version of this work reported a substantially higher figure, which turned out to come from a problem in the data rather than from the model. Retraining on corrected data brought it back to 87%. The lesson was not about the architecture: a number that improves without a reason you can name is a number to check, and I now compare a result against an independent reference before treating it as real.

Implementing adversarial training was also harder than expected. Gradient reversal fails quietly rather than loudly, which forced me into a much more methodical debugging routine than I had used on previous projects.

[GitHub Repository](https://github.com/anasamrouche/Fault-Diagnosis-Project)
