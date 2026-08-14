---
layout: default
title: Liver Cancer Classification from Radiomic Features (Henri Mondor Hospital)
permalink: /projects/henri-mondor/
---

[← Back to home]({{ '/' | relative_url }})

# Liver Cancer Classification from Radiomic Features (Henri Mondor Hospital)

<span class="project-tag">Lab project</span>
<p class="project-meta">Henri Mondor Hospital · CentraleSupélec · Jul 2026</p>

Hepatocellular carcinoma and cholangiocarcinoma call for different treatments but present similarly, and reading the radiomic features extracted from multi-phase contrast MRI is slow work. The task was to find which of those features actually separate the two, on a cohort of 87 against 23 patients with many correlated variables and missing phases.

The main approach was a penalised multi-block logistic regression (groupLASSO), with one block per injection phase (arterial, portal, venous, late) plus blocks of first-order differences between phases. Selection ran over 100 random seeds with stratified 80/20 splits and class weighting for the minority group, which gives averaged performance rather than one lucky split, and a selection frequency per variable. The best configuration reached 93% AUC and 88% accuracy. Random forests and PCA were run alongside as comparison points; the random forest showed the usual trade-off, with high raw accuracy (82%) but a balanced accuracy of only 60%, which matters when the rare class is the one you need to catch.

What made the result convincing was not the metric but the agreement: the most frequently selected variables, portal-phase sphericity and the entropy difference between venous and portal phases, line up with what the oncologists describe qualitatively, and the same variables came back independently through the random forest importances.

[Report]({{ '/assets/Projet_El_Mondor_Radiologie.pdf' | relative_url }})
