---
layout: default
title: Variance Reduction for Monte Carlo Simulation in Financial Mathematics
permalink: /projects/monte-carlo/
---

[← Back to home]({{ '/' | relative_url }})

# Variance Reduction for Monte Carlo Simulation in Financial Mathematics

<span class="project-tag">Course project</span>
<p class="project-meta">CentraleSupélec · Mar 2026</p>

Monte Carlo pricing converges at O(1/√n), so a tenfold gain in precision costs a hundredfold in simulations. The project implemented and compared the main families of variance reduction techniques on European and basket options under Black-Scholes: stratification with Neyman allocation, antithetic variables, importance sampling, control variates, conditioning via the Rao-Blackwell principle, and quasi-Monte Carlo with low-discrepancy sequences.

Rather than stopping at isolated comparisons, we ran a systematic benchmark of 8 methods over 810 parameter configurations spanning dimension, volatility and moneyness, scored by error × √time so that computational overhead counts against a method. Sobol sequences came out best on 46% of configurations, and quasi-Monte Carlo methods collectively on 85%, though plain Monte Carlo recovers ground at low volatility and deep out-of-the-money. Since no method wins everywhere, we trained a random forest on the benchmark to predict the best method from the three parameters, reaching 82% ± 5% cross-validated accuracy, and wrapped it in a pricer that selects the method automatically.

One methodological detail is worth recording: an early version reported 51% accuracy using sequential K-fold cross-validation. The grid was ordered by dimension, so each fold saw only a narrow band of dimensions. Switching to stratified K-fold with shuffling removed the bias and gave the 82% above. The first number was not a worse model, it was a broken evaluation.

[GitHub Repository](https://github.com/Vicosr/Variance-reduction-methods-for-Monte-Carlo-option-pricing)
