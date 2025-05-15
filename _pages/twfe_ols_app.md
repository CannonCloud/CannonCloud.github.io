---
layout: archive
title: "TWFE OLS Interactive App"
permalink: /shiny-app/
author_profile: true
---
## Interactive OLS/TWFE Playground

This page provides access to an interactive application designed for exploring the nuances of estimating treatment effects using traditional Ordinary Least Squares (OLS) with Two-Way Fixed Effects (TWFE) models, especially in settings with staggered adoption **of a binary and terminal treatment**.

**[Click here to launch the TWFE OLS Play Around App](https://cannoncloud.shinyapps.io/TWFE_OLS_Play_Around/)**

### Understanding the Challenges with TWFE

The Two-Way Fixed Effects (TWFE) estimator is a widely used method for causal inference with panel data when treatment is **binary, terminal, and adopted in a staggered fashion across units**. It aims to control for unobserved time-invariant unit-specific confounders (unit fixed effects) and common time-specific shocks (time fixed effects). However, recent econometric research has highlighted several challenges, particularly when treatment effects are heterogeneous across units and over time, and when treatment timing is staggered.

*(It's important to note that while this application focuses on binary and terminal treatments, the challenges discussed can be even more pronounced when dealing with continuous treatments or treatments that are not terminal (i.e., units can switch in and out of treatment). These scenarios introduce further complexities in defining and estimating relevant treatment effect parameters, especially within a staggered adoption framework. For a collection of papers discussing various DiD designs, including those with continuous treatments, see the appendix of Baker, A., Callaway, B., Cunningham, S., Goodman-Bacon, A., & Sant’Anna, P. H. C. (2025), "Difference-in-Differences Designs: A Practitioner’s Guide," available at https://arxiv.org/pdf/2503.13323. For issues related to treatments that are not terminal (treatment switchers), see also De Chaisemartin, C., & D’Haultfœuille, X., "Difference-in-Differences Estimators of Intertemporal Treatment Effects," *The Review of Economics and Statistics*)*

1.  **Heterogeneous Treatment Effects (TE):** When the impact of a **binary, terminal** treatment varies—for instance, differing across treatment cohorts (groups of units treated at the same time) or evolving dynamically over time since treatment exposure—the standard TWFE estimator can produce a weighted average of individualistic treatment effects. This average may not correspond to a parameter of interest and can even be misleading (e.g., biased if dynamic treatment effects are present and not properly accounted for).
2.  **Violations of Parallel Trends Correlated with Treatment Timing:** A core assumption for difference-in-differences (DiD) type estimators, including TWFE, is that treated and control units would have followed parallel trends in the outcome variable in the absence of treatment. If underlying trends differ (e.g., due to unit-specific linear or non-linear time trends) *and these differences are correlated with treatment timing*, TWFE estimates can be severely biased.
3.  **Unobserved Factor Loadings Correlated with Treatment Timing:** If unobserved common factors affect outcomes differently across units (heterogeneous factor loadings), *and these differential sensitivities (factor loadings) are correlated with when units receive treatment*, TWFE may fail to isolate the true treatment effect. This is another form of parallel trends violation, often conceptualized in interactive fixed effect models.

### Explore with the App

This interactive application allows you to simulate panel data (assuming a **binary, terminal treatment**) and observe how these issues affect estimates from TWFE OLS. You can adjust various parameters to create scenarios with:

* **Heterogeneous treatment effects:** Define how the impact of the treatment varies, including setting different effects for various treatment **cohorts** and specifying **dynamic** treatment effect patterns (how effects change over time post-treatment).
* **Violations of parallel trends (correlated with treatment timing):** Introduce differing underlying trends between groups that are linked to when they get treated.
* **Differential factor loadings (correlated with treatment timing):** Simulate scenarios where unobserved common shocks have varied impacts that are linked to treatment timing.

By manipulating these parameters, you can visualize the resulting biases in the TWFE estimator and gain a deeper intuition for when OLS/TWFE fails and how badly.

### Alternative Estimators Available in this App

This app implements two robust, recently developed estimators designed to address the shortcomings of TWFE when dealing with **binary, terminal treatments** in staggered adoption settings:

* **Borusyak, Jaravel, and Spiess (BJS, 2023) Imputation Estimator:** This estimator imputes counterfactual outcomes for treated units based on untreated units. It's particularly well-suited for handling heterogeneous treatment effects.
* **Synthetic Difference-in-Differences (SDID) by Arkhangelsky, Athey, Hirshberg, and Imbens (2021):** This estimator generalizes the synthetic control method to a difference-in-differences framework, re-weighting control units to match pre-treatment trends.

These estimators, BJS and SDID, are part of a broader family of modern "robust" DiD methods that share common goals in improving upon traditional TWFE. Generally, these advanced estimators—including others in the literature like Callaway and Sant'Anna (CS, 2021) and the Wooldridge (2021) Mundlak-style approach—strive for several key improvements:
1.  **Identification Strategy - Avoiding "Forbidden Comparisons":** They ensure that for estimating the effect on a particular group of treated units, other already-treated units are not used as part of the control group, thus avoiding the "negative weighting" problem.
2.  **Meaningful Aggregation of Treatment Effects:** They focus on clearly defined average treatment effects on the treated (ATTs) for specific cohorts and time periods.
3.  **Inference and Standard Errors:** They often make more explicit assumptions about the error structure or provide robust procedures for more reliable inference.

While the specific assumptions and mechanics differ across this family of estimators, they are highly related, for example BJS is a unique case of the Mundlak estimator, and BJS and CS are equivalent if there is only one pretreatment period. The choice among them should ideally be guided by the specific research question, data characteristics, and how well an estimator's assumptions align with the plausible Data Generating Process (DGP) for the study.

The **BJS estimator** is included in this app partly because it readily allows for the incorporation of unit-specific linear time trends, which can be crucial for addressing certain types of parallel trends violations. It is also the most efficient as its imputation approach can leverage all available pre-treatment periods (unlike CS) and flexibly use all not-yet-treated units as controls. SDID, in contrast, is uniquely well suited for estmation with factor models.

Experiment with BJS and SDID in the app to see how they perform under different data generating processes you define. This can help illustrate their respective strengths and limitations in practical scenarios.

I encourage you to create the most messed up plots you can, and hopefully learn something!
