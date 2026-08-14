---
layout: default
title: Multi-view Sport Video Synchronisation (GoPro)
permalink: /projects/gopro-synchformer/
---

[← Back to home]({{ '/' | relative_url }})

# Multi-view Sport Video Synchronisation (GoPro)

<span class="project-tag">Client project</span>
<p class="project-meta">GoPro · CentraleSupélec · Synchformer track · Jan 2026 – Jun 2026</p>

## Problem

When the same scene is filmed by several cameras at once, the streams start at arbitrary offsets. Without a shared timecode or a clapperboard, they cannot be aligned directly, and the alignment has to be recovered from the content itself. The client context was the GoPro Quik mobile app, where users assemble multi-angle footage of sports sessions.

Classical audio cross-correlation breaks down here: wind noise, saturation and the absence of any continuous sound track make the audio unreliable in exactly the conditions action cameras are used in.

## Approach

The team surveyed the literature and retained three complementary architectures: Synchformer (audio-visual, built to exploit sparse cues such as impacts), SeSyn-Net (self-supervised, based on 2-D human pose and therefore view-invariant), and VideoSync (frame-embedding similarity). I worked on the Synchformer track.

The first step was deploying the model on the CentraleSupélec GPU cluster (DGX A100, jobs submitted through SLURM): adapting the authors' code to the infrastructure, handling CUDA dependencies, and writing submission scripts for the available MIG partitions. Inference on HD video kept running out of system memory because frames were loaded in full, which I resolved by pre-encoding every video to the format the model expects (25 fps, 256 px, 16 kHz audio) and splitting long videos into 10-second segments processed as independent jobs.

Fine-tuning targeted Phase II of the training scheme only: the AST and Motionformer feature extractors stay frozen and just the lightweight synchronisation module is trained, starting from the authors' AudioSet checkpoint. The corpus was around 7,000 ten-second segments from Ego-Exo4D, chosen because it combines exocentric GoPro cameras with egocentric Aria Glass footage in real conditions. Training ran roughly 20 hours on a single MIG partition.

## Evaluation

Testing used 213 takes across 13 activity classes. For each take a random offset in [−2.0 s, +2.0 s] is applied between the video and audio streams, the model runs on sliding 10-second windows, and the per-segment predictions are aggregated. I compared two aggregation strategies: keeping the prediction of the most confident segment (0.487 s MAE) against a confidence-weighted average of all of them (0.583 s MAE). Diluting uninformative segments into an average makes things worse, which is the first useful finding.

The second is that performance splits sharply by activity type. Continuous audio-visual signals (music, dance, football) give MAE between 1.00 s and 1.80 s, while activities built around discrete events (cooking, CPR, manual tasks) land at or near the 0.2 s resolution of the classification grid.

The third, and the one that matters most in production, is that the model's confidence score is well calibrated against actual accuracy: takes above 0.8 confidence, 54% of the sample, have a 0.115 s MAE, against 1.165 s below 0.5. This score is the softmax maximum of the classification layer, an intrinsic output rather than a metric computed after the fact, so it can be used directly as a routing signal to hand a low-confidence clip over to a pose-based method.

Combining both filters (discrete-event activities, confidence above 0.8) isolates 89 takes on which the model reaches 0.081 s MAE, below the discretisation step of the grid.

## What I took from it

No single model solves the problem across all conditions, and the deliverable that actually served the client was the comparative benchmark: which model to use, under which conditions, and with which reliability indicator. Stating a headline number without the conditions attached would have been useless to them.

The engineering side is what I learned most from: large datasets on a shared cluster, GPU memory failures, and adapting research code to an infrastructure it was never written for.

[Analysis Report]({{ '/assets/Rapport_de_projet.pdf' | relative_url }})
