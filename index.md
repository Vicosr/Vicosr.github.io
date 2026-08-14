---
layout: default
title: Home
---

<p class="availability"><span class="availability-label">Availability.</span> 5-6 month gap-year internship (stage de césure), starting September 2026.</p>

# About Me

Hello, my name is Victor Roussel. I am a student in the General Engineering program at CentraleSupélec, Université Paris-Saclay, majoring in mathematics.

My mathematical background (algebra, analysis, probability) is the common thread behind everything I work on. I apply it mostly to machine learning, signal processing and quantitative finance, with detours through cryptography.

## Stack

**Languages & libraries:** Python (NumPy, Pandas, scikit-learn, PyTorch), R, MATLAB, OCaml, SQL

**Infrastructure:** Slurm, DGX A100, Git, Bash

## Khôlles

Alongside my studies, I give weekly oral examinations (khôlles) to CPGE students preparing for France's engineering school entrance exams: 6 students a week in mathematics, at Lycée Hoche. [See what this involves, with examples →]({{ '/kholles/' | relative_url }})

# Projects

The write-ups below go into different levels of detail. The fault diagnosis and video synchronisation projects include the full method and evaluation; the other two are summarised in a paragraph.

<div class="project-list" markdown="1">

<div class="project-entry" markdown="1">
<a class="project-title" href="{{ '/projects/fault-diagnosis/' | relative_url }}">Robot Fault Diagnosis via Sim-to-Real Domain Adaptation</a>
<p class="project-meta"><span class="project-tag">Lab project</span> · CentraleSupélec LGI · Jan 2025 – Jun 2025</p>

Trained a fault classifier on simulated robot data and transferred it to real sensor data with a DANN, reaching 93.97% ± 2.54% accuracy over five runs against an 86% baseline, from 90 real samples in total.
</div>

<div class="project-entry" markdown="1">
<a class="project-title" href="{{ '/projects/gopro-synchformer/' | relative_url }}">Multi-view Sport Video Synchronisation (GoPro)</a>
<p class="project-meta"><span class="project-tag">Client project</span> · GoPro · Jan 2026 – Jun 2026</p>

Fine-tuned a Synchformer-based model on Ego-Exo4D on DGX A100 / Slurm infrastructure, and showed its confidence score to be calibrated enough to act as a routing signal between synchronisation methods.
</div>

<div class="project-entry" markdown="1">
<a class="project-title" href="{{ '/projects/henri-mondor/' | relative_url }}">Liver Cancer Classification from Radiomic Features (Henri Mondor Hospital)</a>
<p class="project-meta"><span class="project-tag">Lab project</span> · Henri Mondor Hospital · Jul 2026</p>

Identified which multi-phase MRI radiomic features separate two liver cancers on an imbalanced cohort, reaching 93% AUC with features that matched the oncologists' own reading.
</div>

<div class="project-entry" markdown="1">
<a class="project-title" href="{{ '/projects/monte-carlo/' | relative_url }}">Variance Reduction for Monte Carlo Simulation in Financial Mathematics</a>
<p class="project-meta"><span class="project-tag">Course project</span> · Mar 2026</p>

Benchmarked 8 variance reduction methods across 810 option pricing configurations, then trained a classifier to pick the best method for a given set of market parameters.
</div>

</div>
