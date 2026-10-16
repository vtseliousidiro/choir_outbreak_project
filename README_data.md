# Data: Skagit County Choir COVID-19 Outbreak

## Source
**Primary reference:** Hamner L, Dubbel P, Capron I, et al. "High SARS-CoV-2 Attack Rate Following Exposure at a Choir Practice — Skagit County, Washington, March 2020." *MMWR Morb Mortal Wkly Rep*. 2020;69(19):606–610. https://doi.org/10.15585/mmwr.mm6919e6

All numbers in `outbreak_data.csv` were transcribed by hand from this report. There is no raw or individual-level data, and no script fetches it.

## `outbreak_data.csv`
17 rows, one per quantity. Columns:
- `parameter`: variable name
- `value`: number
- `unit`: unit, or `dimensionless`
- `source`: citation
- `note`: definition or denominator

## What the numbers mean
- **Event:** a 2.5-hour (150 min) choir practice on 10 March 2020; 61 of 122 members attended. One attendee (the index patient) had symptoms from 7 March.
- **Cases:** 53 including the index patient (33 confirmed, 20 probable), i.e. **52 secondary cases** (32 confirmed, 20 probable) among the **60** other attendees. Probable cases were not tested.
- **Attack rate:** 52/60 = 86.7% (confirmed + probable); 32/60 = 53.3% (confirmed only).
- **Onset:** 1–12 days after the practice (median 3 days); 49 of 53 (92.5%) on 11–15 March.
- **Seating:** six rows of 20 chairs, 6–10 inches apart.
- **Outcomes:** 3 of 53 hospitalised, 2 of 53 died. Denominator is all 53 cases, including the index patient.

## Notes and caveats
- The report gives 33 confirmed cases in the text and 32 confirmed secondary cases in the summary; the report does not reconcile them, but 33 + 20 = 53 total cases and 32 + 20 = 52 secondary cases, which is consistent with the index patient being the extra confirmed case. The report's summary gives the death rate as 3.7% and the text as 3.8% (both 2/53); the CSV uses 0.038.
- The seating chart and spatial distribution of cases are not published (withheld for privacy), so spatial arguments cannot be checked from this data.
- Ventilation, temperature and humidity are not reported in the paper.
- The index patient also attended the 3 March practice (78 attendees); this is not modelled.
- The notebook uses `n_exposed`, `n_secondary_cases`, `n_confirmed`, `exposure_duration` and the three incubation rows. The other rows are context only.
