---
layout: archive
title: "TWFE OLS Interactive App"
permalink: /shiny-app/
author_profile: true
---
## Interactive TWFE OLS Playground

This page provides access to an interactive application designed for exploring the nuances of estimating treatment effects using traditional Ordinary Least Squares (OLS) with Two-Way Fixed Effects (TWFE) models, especially in settings with staggered treatment adoption.

**[Click here to launch the TWFE OLS Play Around App](https://cannoncloud.shinyapps.io/TWFE_OLS_Play_Around/)**

### Understanding the Challenges with TWFE

The Two-Way Fixed Effects (TWFE) estimator is a widely used method for causal inference with panel data. It aims to control for unobserved time-invariant unit-specific confounders (unit fixed effects) and common time-specific shocks (time fixed effects). However, recent econometric research has highlighted several challenges, particularly when treatment effects are heterogeneous across units and over time, and when treatment timing is staggered:

1.  **Heterogeneous Treatment Effects (TE):** When the impact of a treatment varies—for instance, differing across treatment cohorts (groups of units treated at the same time) or evolving dynamically over time since treatment exposure—the standard TWFE estimator can produce a weighted average of individualistic treatment effects. This average may not correspond to a parameter of interest and can even be misleading (e.g., biased if dynamic treatment effects are present and not properly accounted for).
2.  **Violations of Parallel Trends Correlated with Treatment Timing:** A core assumption for difference-in-differences (DiD) type estimators, including TWFE, is that treated and control units would have followed parallel trends in the outcome variable in the absence of treatment. If underlying trends differ (e.g., due to unit-specific linear or non-linear time trends) *and these differences are correlated with treatment timing*, TWFE estimates can be severely biased.
3.  **Unobserved Factor Loadings Correlated with Treatment Timing:** If unobserved common factors affect outcomes differently across units (heterogeneous factor loadings), *and these differential sensitivities (factor loadings) are correlated with when units receive treatment*, TWFE may fail to isolate the true treatment effect. This is another form of parallel trends violation, often conceptualized in interactive fixed effect models.

### Explore with the App

This interactive application allows you to simulate panel data and observe how these issues affect estimates from TWFE OLS. You can adjust various parameters to create scenarios with:

* **Heterogeneous treatment effects:** Define how the impact of the treatment varies, including setting different effects for various treatment **cohorts** and specifying **dynamic** treatment effect patterns (how effects change over time post-treatment).
* **Violations of parallel trends (correlated with treatment timing):** Introduce differing underlying trends between groups that are linked to when they get treated.
* **Differential factor loadings (correlated with treatment timing):** Simulate scenarios where unobserved common shocks have varied impacts that are linked to treatment timing.

By manipulating these parameters, you can visualize the resulting biases in the TWFE estimator and gain a deeper intuition for when OLS/TWFE fails and how badly.

### Alternative Estimators

The app also includes more robust, recently developed estimators designed to address some of the shortcomings of TWFE:

* **Borusyak, Jaravel, and Spiess (BJS, 2023) Imputation Estimator:** This estimator is particularly well-suited for handling heterogeneous treatment effects. When combined with unit-specific linear time trends, it can also effectively address certain violations of the parallel trends assumption.
* **Synthetic Difference-in-Differences (SDID) by Arkhangelsky, Athey, Hirshberg, and Imbens (2021):** This estimator generalizes the synthetic control method to a difference-in-differences framework. It re-weights control units to match the pre-treatment trends of treated units and estimates weights for time periods to balance pre-treatment outcomes. SDID can be robust to certain forms of unobserved confounding (violations of parallel trends and issues with heterogeneous factor loadings), particularly when a good synthetic control can be constructed from the donor pool of untreated units.

Experiment with these alternative estimators in the app to see how they perform under different data generating processes you define. This can help illustrate their strengths and limitations in practical scenarios.

I encourage you to create the most messed up plots you can, and hopefully learn something!
