# Data: Skagit County Choir COVID-19 Outbreak

## Source
**Primary reference:** Hamner L, Dubbel P, Capron I, et al. "High SARS-CoV-2 Attack Rate Following Exposure at a Choir Practice — Skagit County, Washington, March 2020." *Morbidity and Mortality Weekly Report*. 2020;69(19):606–610. https://doi.org/10.15585/mmwr.mm6919e6

**Secondary mechanistic reference:** Miller SL, Nazaroff WW, Jimenez JL, et al. "Transmission of SARS-CoV-2 by inhalation of respiratory aerosol in the Skagit Valley Chorale superspreading event." *Indoor Air*. 2020. Submitted.

## Data Description

### outbreak_data.csv
Extracted epidemiological and environmental parameters from the March 10, 2020 rehearsal.

**Columns:**
- `parameter`: Variable name
- `value`: Numerical value
- `unit`: SI units or dimensionless
- `source`: Citation
- `note`: Context or derivation

**Key observations:**
- **Attack rate:** 52/60 susceptible attendees infected (86.7%)
- **Exposure:** Single 2.5-hour singing practice
- **Spatial distribution:** Cases broadly distributed throughout room (no clustering near index patient)
- **Incubation:** Median 3 days; 92.5% with symptom onset within 1–5 days post-exposure
- **Mechanism:** Airborne transmission likely (contact/fomite modes implausible given spatial distribution and precautions taken)

## Processing Notes

1. **Index patient exclusion:** Attack rate calculated as secondary cases / susceptible = 52 / (61-1) = 86.7%
2. **Case definitions:** 32 confirmed by RT-PCR; 20 probable (clinically compatible + epidemiologic link, per CSTE criteria)
3. **Incubation timing:** Derived from reported symptom onset dates (March 11–15) relative to exposure (March 10)
4. **No raw individual-level data:** Published aggregated statistics; seating chart withheld for privacy

## Limitations

- Single outbreak; not representative of all transmission scenarios
- Singing is a high-risk activity (aerosol emission); generalization to routine indoor meetings limited
- Viral load, breathing rates, and exact occupant positions not reported
- Environmental parameters (ventilation, temperature, humidity) poorly characterized
