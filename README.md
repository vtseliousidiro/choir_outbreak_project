# Modeling Transmission Dynamics of the Skagit County Choir COVID-19 Outbreak

**Course:** CB2330 Scientific Computing for Life Sciences, PRO1 Project  


## Overview

This project applies probabilistic modeling, parameter estimation, and uncertainty quantification to the Skagit County Choir superspreading event (March 10, 2020).

**Core research question:** Given an observed 86.7% attack rate from a 2.5-hour singing exposure, what transmission rate **β** (per minute) explains this data, and how certain are we?

**Methods:** Gradient descent (maximum likelihood estimation) and Bayesian MCMC (Metropolis-Hastings).

## Key Findings

- **Fitted transmission rate:** β ≈ 0.005 per minute (frequentist MLE)
- **95% Confidence interval:** [0.003, 0.008] per minute
- **Bayesian posterior:** β ∈ [0.004, 0.007] per minute (credible interval)
- **Model validation:** Posterior predictive checks show good agreement with observed 52 secondary cases
- **Sensitivity:** Attack rate increases predictably with exposure duration (30 min → ~30%, 150 min → ~87%)

## Repository Structure

```
choir_outbreak_project/
├── README.md                 ← This file
├── project.ipynb             ← Full analysis notebook
├── data/
│   ├── README.md            ← Data source & format documentation
│   └── outbreak_data.csv    ← Extracted epidemiological parameters
└── .gitignore               ← (Excludes generated plots, cache)
```

## How to Run

### Requirements
```bash
pip install numpy pandas scipy matplotlib seaborn
```

### Execution
```bash
jupyter notebook project.ipynb
```

The notebook runs top-to-bottom without manual edits. Cell 1 loads all imports and data. Subsequent cells:

1. **Data & Model Setup** — Load outbreak data, define transmission model
2. **Incubation Period Fit** — Lognormal distribution for symptom onset timing
3. **Gradient Descent (MLE)** — Fit β using L-BFGS-B optimizer
4. **Likelihood Scan** — Compute confidence intervals via likelihood ratio test
5. **Bayesian MCMC** — Metropolis-Hastings sampler for full posterior
6. **Diagnostics** — Trace plots, autocorrelation, posterior density
7. **Posterior Predictive Checks** — Validate model against observed data
8. **Sensitivity Analysis** — Attack rate vs. exposure duration
9. **Summary** — Comparison of frequentist and Bayesian results

Generated plots saved as PNG files (01–06_*.png) in working directory.

## Model

### Generative Model
```
P(infection | t, β) = 1 - exp(-β·t)
```

**Interpretation:** Assumes Poisson process for virus particle transmission. Each minute of exposure, the susceptible person is "hit" by an average of β virus particles. Infection occurs if ≥1 particle successfully infects.

### Parameters
| Parameter | Symbol | Units | Range (fitted) | Interpretation |
|-----------|--------|-------|----------------|-----------------|
| Transmission rate | β | per minute | 0.005 (0.003–0.008) | Virus transmission efficiency under close-proximity singing |
| Exposure duration | t | minutes | 150 (observed) | Time in shared air with infectious person |

### Assumptions
1. **Poisson transmission:** Constant rate, independent events
2. **Well-mixed room:** Index patient's emissions evenly distributed (supported by broad spatial distribution of secondary cases)
3. **Constant viral load:** Index patient shedding rate stable over 2.5 hours (reasonable; ~3 days post-symptom onset)
4. **No reinfection:** Each person infected at most once during exposure
5. **Homogeneous susceptibility:** All attendees equally susceptible (ignores age, immunity, etc.)

## What This Adds to the Paper

The original Hamner et al. paper **reports** the outbreak:
- 52 out of 60 people got infected
- Attack rate is 86.7%
- Argues airborne transmission is likely

**This project:** 
- **Infers** the underlying transmission rate (β) from the attack rate
- **Quantifies uncertainty** via frequentist and Bayesian methods
- **Compares approaches:** Gradient descent vs. MCMC on same data
- **Validates model:** Posterior predictive checks confirm fit
- **Explores robustness:** Sensitivity to exposure duration
- **Mechanistic grounding:** Connects to Wells-Riley aerosol model (Miller et al. 2020)

## Model Limitations & Failure Modes

1. **Single parameter:** β aggregates ventilation, viral load, breathing rate, room geometry into one number. Cannot predict effect of interventions (e.g., "what if we increased ventilation?") without additional data.

2. **No incubation coupling:** Incubation model (lognormal, 3-day median) is separate from transmission model. In reality, probability of infection depends on timing of exposure relative to infectious period.

3. **Homogeneity:** Ignores:
   - **Viral load heterogeneity:** Superemitters release ≥10× more virus (Asadi et al. 2019)
   - **Positional differences:** Index patient's exact location in room unknown; assumed effect averaged
   - **Activity-dependent breathing:** Singers emit more aerosol than speakers

4. **Superspreading atypicality:** 86.7% attack rate is extreme. Generalization to routine indoor activities (offices, classrooms) unjustified.

5. **One outbreak:** No cross-validation. β fitted to single event; cannot assess reproducibility without independent outbreak data.

6. **Environmental uncertainty:** Ventilation, temperature, humidity not directly measured. Miller et al. estimate ventilation rate ≈ 0.3–1.0 h⁻¹; actual value affects true β.

7. **No accounting for partial immunity:** Some attendees may have prior infection or vaccination (unlikely in March 2020, but relevant for modern outbreaks).

## References

1. Hamner L, Dubbel P, Capron I, et al. "High SARS-CoV-2 Attack Rate Following Exposure at a Choir Practice — Skagit County, Washington, March 2020." *MMWR Morb Mortal Wkly Rep*. 2020;69(19):606–610.

2. Miller SL, Nazaroff WW, Jimenez JL, et al. "Transmission of SARS-CoV-2 by inhalation of respiratory aerosol in the Skagit Valley Chorale superspreading event." *Indoor Air*. 2020 (submitted).

3. Asadi S, Wexler AS, Cappa CD, et al. "Aerosol Emission and Superemission During Human Speech Increase with Voice Loudness." *Sci Rep*. 2019;9:2348.

## Contact

For questions: See project.ipynb notebook for detailed documentation.

---

**Last updated:** Sept 30, 2026  
**Status:** Exhibition-ready ✓
