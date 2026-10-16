# Modeling Transmission Dynamics of the Skagit County Choir COVID-19 Outbreak

CB2330 Scientific Computing for Life Sciences, PRO1 project (autumn 2026).

## What this is
A one-parameter generative model of the secondary attack rate in the Skagit County choir outbreak (Hamner et al., MMWR 2020): each of the 60 other attendees is infected with probability p = 1 − exp(−β·t), t = 150 min, so the number of secondary cases is Binomial(60, p). The model is simulated forwards, then β is estimated from the reported 52 secondary cases (32 confirmed + 20 probable) with maximum likelihood and with a grid-based Bayesian posterior.

## What it found
Caveat first: the model has one parameter and one data point, so the fit is exact by construction and the posterior predictive check cannot falsify it. The estimate depends on counting the 20 probable (untested) cases; with confirmed cases only (32/60 = 53.3%), β ≈ 0.0051/min.

| Quantity | Value |
|---|---|
| β, maximum likelihood (L-BFGS-B) | 0.0134 /min |
| 95% interval, likelihood ratio (Wilks) | [0.0099, 0.0180] /min |
| β, posterior mean (Gamma(1, scale 1/100) prior) | 0.0134 /min |
| 95% credible interval, grid posterior | [0.0096, 0.0181] /min |
| Posterior predictive secondary cases, 95% interval | 43–58 (observed: 52) |
| Attack rate at the posterior median β for 30 / 60 / 150 min | 33% / 55% / 86% (extrapolation; only 150 min is observed) |

β = 0.005/min is only the initial guess in the notebook; it predicts ~53% against 86.7% observed.

## Repository structure
```
choir_outbreak_project/
├── README.md             <- this file
├── project.ipynb         <- project card, then the analysis
├── requirements.txt
├── .gitignore
└── data/
    ├── README.md         <- source, definitions and caveats of the numbers
    └── outbreak_data.csv <- aggregate numbers from Hamner et al. 2020
```

## How to run
```
pip install -r requirements.txt
jupyter notebook project.ipynb
```
Run all cells from the top; the notebook reads `data/outbreak_data.csv` relative to its own folder and needs no edits. Random seed is fixed. The figures (`01`–`07_*.png`) are written to the working directory and are also embedded in the notebook; they are git-ignored.

## Notebook contents
1. Data loading
2. Exposure-to-onset interval (lognormal, descriptive only)
3. Transmission model (derivation)
4. Forward simulation (β = 0.005/min)
5. Maximum likelihood (L-BFGS-B) and forward simulation at the MLE
6. Likelihood scan and 95% interval
7. Bayesian grid posterior
8. Posterior and comparison with the frequentist interval
9. Posterior predictive simulation
10. Exposure-duration scenarios
11. Summary

## Assumptions and limitations (short version; full list in the project card)
Constant-rate Poisson transmission with single-hit infection; well-mixed room and equal exposure for all attendees (not checkable: the paper does not publish a seating chart); only the 10 March practice is modelled; probable cases counted as infections. β lumps emission, breathing, ventilation and room geometry together and does not transfer to other rooms. One outbreak, selected for being extreme, so β is possibly biased high and cannot be tested for reproducibility.

## References
1. Hamner L, Dubbel P, Capron I, et al. High SARS-CoV-2 Attack Rate Following Exposure at a Choir Practice — Skagit County, Washington, March 2020. *MMWR Morb Mortal Wkly Rep*. 2020;69(19):606–610. https://doi.org/10.15585/mmwr.mm6919e6
2. Miller SL, Nazaroff WW, Jimenez JL, et al. Transmission of SARS-CoV-2 by inhalation of respiratory aerosol in the Skagit Valley Chorale superspreading event. *Indoor Air*. 2021;31(2):314–323. https://doi.org/10.1111/ina.12751 (functional form of the model follows the Wells–Riley approach used in analyses of this event; no comparison of β with their estimates is made)
