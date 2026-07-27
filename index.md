---
layout: default
title: Home
---
# About Me
Hello, my name is Victor Roussel. I am a student in the General Engineering program at CentraleSupélec, Université Paris-Saclay, majoring in mathematics.
My mathematical background — algebra, analysis, probability — is the common thread behind everything I work on. I choose my coursework and projects across domains such as:
- AI / Machine Learning
- Data Science
- Signal Processing & Applied Mathematics
- Finance
- Cryptography
- Computer Science
Below, you will find some of the projects I have worked on, as well as the oral examinations (khôlles) I give to CPGE students preparing for France's engineering school entrance exams.
# About The Khôlles
You may have seen on my CV that I give oral examinations at Lycée Hoche (Versailles, France). Since this role is part of the French CPGE system, which is specific to France, I wanted to elaborate.
CPGE is an intensive two-year undergraduate program in mathematics and physics, preparing students for nationwide competitive entrance exams to top French engineering schools. Throughout the program, students have weekly oral mock exams to prepare them for the entrance exams and assess their understanding of the courses.
My role is to conduct such exams for 6 students each week. I prepare course questions and exercises specially tailored for the students I am examining. You can see some examples just below.
## Examination Examples
- [Probability (Week 14)](/assets/week14_probability.pdf)
- [Matrix Decomposition (Week 12)](/assets/week12_matrix_decomposition.pdf)
- [Power Series (Week 6)](/assets/week06_power_series.pdf)
# Projects
## Course project: Liver Cancer Classification from Radiomic Features — Henri Mondor Hospital
*Jul 2026*
Distinguished two types of liver cancer (hepatocellular carcinoma vs. cholangiocarcinoma) from multi-phase MRI radiomic features, on an imbalanced cohort (87 vs. 23 patients). Compared three approaches — penalized multi-block regression (groupLASSO), random forests, and PCA — with explicit class-imbalance correction and stratified resampling across 100 random seeds. Best configuration reached 93% AUC and 88% accuracy.
[Report](/assets/Projet_El_Mondor_Radiologie.pdf) 

## Course project: Robot Fault Diagnosis through Transfer Learning and Digital Twins — CentraleSupélec LGI
*Jan 2025 -- Jun 2025*
Explored the feasibility of classifying real faults on a mechanical arm using a classifier trained on simulated data. Achieved 87% AUC using a DANN built on a 1D-CNN architecture.
[GitHub Repository](https://github.com/anasamrouche/Fault-Diagnosis-Project)
## Course project: Multi-view Sport Video Synchronisation — GoPro
*Jan 2026 -- Jun 2026*
Fine-tuned a Synchformer-based model for automatic multi-view audio-visual synchronisation on the Ego-Exo4D dataset, comparing human pose detection, audio-based alignment using transformers, and visual similarity matching. Achieved a mean absolute error of 0.081s on a high-confidence, discrete-activity subset of 89 takes.
[Analysis Report](/assets/Rapport_de_projet.pdf)
## Course project: Variance Reduction for Monte Carlo Simulation in Financial Mathematics
*Mar 2026*
Explored low-discrepancy sequences as alternatives to standard Monte Carlo methods. Found that Sobol sequences were the most efficient in 46% of configurations; trained a random forest achieving 81% CV accuracy to predict the best method for a given configuration.
[GitHub Repository](https://github.com/Vicosr/Variance-reduction-methods-for-Monte-Carlo-option-pricing)