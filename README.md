# Young Driver Collision Severity Analysis

## Overview

This repository contains the Python/Jupyter Notebook analysis supporting an Open University TM470 EMA project on road traffic collision severity involving young car drivers.

The project uses **Department for Transport STATS19 road safety data** and examines collisions involving **17–19-year-old car drivers in England and Wales between 2018 and 2024**.

### Research question

> To what extent are specific driving conditions and collision characteristics associated with higher-severity road traffic collisions involving 17–19-year-old car drivers in England and Wales between 2018 and 2024, and how do combinations of these factors relate to collision severity?

## Characteristics examined

- Night-time conditions
- Weekend status
- Young-passenger presence
- Driver sex
- Vehicle age

Vehicle age is analysed at driver–vehicle level because some collisions contain more than one qualifying young driver. The primary collision-level statistical and machine-learning analyses therefore use the four characteristics that can be represented consistently at collision level.

## Outcome

The analysis uses the STATS19 `collision_severity` variable consistently across 2018–2024:

- **Higher severity:** Fatal or Serious
- **Lower severity:** Slight

The project deliberately uses the legacy severity classification rather than the later enhanced severity categories so that the outcome remains comparable across the whole study period.

## Main findings

The final analysis contains:

- **35,799** unique qualifying collisions
- **7,754** higher-severity collisions
- **28,045** lower-severity collisions
- **36,586** qualifying young-driver/vehicle records

The clearest individual association was young-passenger presence, followed by night-time conditions and driver sex. Vehicle age showed a statistically supported but very small association, while weekend status showed insufficient evidence of an association.

Predictive discrimination was limited:

| Model | Held-out ROC-AUC | Five-fold CV mean ROC-AUC |
|---|---:|---:|
| Logistic regression | 0.567 | 0.578 |
| Decision Tree | 0.570 | 0.579 |
| Random Forest | 0.570 | 0.579 |

These results should be interpreted as **associations and predictive performance**, not evidence of causation or individual risk.

## Repository contents

```text
young-driver-collision-analysis/
├── Project-EMA-final.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Data source

The analysis uses the Department for Transport's STATS19 road safety open data:

https://www.gov.uk/government/statistical-data-sets/road-safety-open-data

The raw STATS19 CSV files are **not included in this repository** because they are very large. The notebook downloads the published datasets directly and then restricts the data to the 2018–2024 study period and England/Wales young-driver study population.

Because the Department for Transport periodically updates and revises published data, running the notebook at a later date may not reproduce every record exactly. The reported EMA results are based on the data available when the analysis was conducted.

## Running the notebook

1. Install Python 3.10+.
2. Install the required packages:

```bash
pip install -r requirements.txt
```

3. Open `Project-EMA-final.ipynb` in Jupyter Notebook, JupyterLab or another compatible notebook environment.
4. Run the cells from top to bottom.

The notebook downloads the STATS19 data from the Department for Transport, so an internet connection is required for the data-acquisition cell.

The full STATS19 files are large. Allow sufficient disk space, memory and download time.

## Analytical workflow

The notebook follows this sequence:

1. Load and inspect STATS19 collision, vehicle and casualty data.
2. Restrict collision records to England and Wales and the study period.
3. Identify qualifying car drivers aged 17–19.
4. Harmonise collision severity.
5. Derive night-time, weekend and young-passenger indicators.
6. Construct collision-level and driver–vehicle-level datasets.
7. Explore individual characteristics using descriptive statistics.
8. Use chi-square tests and Cramér's V to assess unadjusted associations.
9. Use multivariable logistic regression to assess adjusted associations.
10. Use logistic regression, Decision Tree and Random Forest models to evaluate predictive discrimination.
11. Examine combinations of characteristics using descriptive collision profiles.
12. Run final validation checks.

## Reproducibility and interpretation

The project distinguishes between:

- **statistical association**, which assesses whether groups differ in observed severity;
- **adjusted association**, which considers several characteristics simultaneously; and
- **prediction**, which assesses discrimination on unseen observations.

The analysis does not claim that any selected characteristic causes a collision or determines an individual's risk.

## Software

The analysis was developed using Python, pandas, NumPy, SciPy, statsmodels, scikit-learn and Matplotlib.

Tableau was used separately for the project's dashboard and communication of results.
## Tableau dashboard

The repository includes a Tableau dashboard summarising the collision-level findings from the project.

- **Dashboard:** `tableau/young-driver-collision-dashboard.twbx`
- **Collision-level Tableau data:** `tableau/tableau_data.csv`
- **Combined-profile Tableau data:** `tableau/tableau_profiles.csv`

The dashboard covers 35,799 collisions involving qualifying 17–19-year-old car drivers in England and Wales from 2018–2024. Higher severity combines fatal and serious collisions; lower severity represents slight collisions.

The dashboard presents observed higher-severity proportions by:

- young-passenger presence
- lighting condition
- day type
- driver sex
- year

It also presents descriptive comparisons of the highest- and lowest-rate combinations of the selected characteristics.

The results represent observed associations rather than causal effects. Vehicle age is analysed separately at driver–vehicle level in the EMA because it cannot always be uniquely assigned to a collision.

The Tableau dashboard is provided as a supplementary visualisation of the analysis; the Jupyter Notebook remains the main computational record of the project.
