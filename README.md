## Repository structure

```
WHR_and_Blood_Pressure_repo/
├── README.md
├── requirements.txt
├── data/
│   └── nhanes/
│       ├── *.xpt
│       └── *.csv.gz
├── notebooks/
│   ├── Report_1_haochuns.ipynb
│   ├── sbp_dr.ipynb
│   ├── sbp_gam.ipynb
│   ├── sbp_krr.ipynb
│   ├── sbp_lm.ipynb
│   └── corresponding .Rmd files
├── scripts/
│   ├── python/
│   ├── r/
│   └── julia/
├── reports/
│   └── haochuns_stats_504_assignment_1.pdf
└── assets/
    ├── figures/
    └── source_images/
```

# Waist-to-Hip Ratio, Waist Circumference, and Blood Pressure in NHANES

This project studies how central adiposity is associated with systolic blood pressure using NHANES 2017–March 2020 pre-pandemic data. The analysis focuses on adults and compares several functional forms for body-size effects, with particular attention to waist circumference, waist-to-hip ratio, sex differences, and nonlinear patterns.

## Project goal

The main question is whether blood pressure rises in a simple linear way with abdominal body shape measures, or whether the relationship is nonlinear and differs across subgroups. To answer that, the notebook compares linear, polynomial, and spline-based specifications and visualizes the fitted relationships.

## Data

Source: `nhanes_2017_march2020.csv`

Key variables used in the analysis include:

- `AvgBP` as the outcome variable for average systolic blood pressure
- `BMXWAIST` for waist circumference
- `BMXHIP` for hip circumference
- `WHR` for waist-to-hip ratio
- `RIDAGEYR` for age
- `BMXBMI` for BMI
- `INDFMPIR` for poverty-income ratio
- `RIAGENDR` for sex
- `RIDRETH1` for race/ethnicity

The notebook restricts to adults and removes missing values for the variables needed in each model.

## Methods

The workflow combines descriptive visualization and regression modeling:

1. Explore the raw relationship between anthropometric measures and blood pressure.
2. Fit nested mean models for systolic blood pressure using waist circumference with increasing flexibility.
3. Compare linear, quadratic, cubic, and spline-based specifications using AIC, BIC, adjusted R-squared, partial F tests, and Wald tests.
4. Add covariate adjustment for age, BMI, sex, race/ethnicity, and income.
5. Visualize fitted curves to check whether the relationship is approximately linear or meaningfully nonlinear.

A key result from the notebook is that spline models provide the best overall fit among the candidate specifications, with the natural spline model with 4 degrees of freedom giving the lowest AIC in the main comparison. The analysis also finds evidence that the waist effect differs by sex.

## Main takeaways

- Waist circumference is positively associated with systolic blood pressure, but the pattern is not perfectly linear.
- More flexible models improve fit over a simple linear specification.
- A natural spline with 4 degrees of freedom gives the strongest fit among the compared models in the notebook output.
- The waist–blood pressure relationship appears steeper in some ranges of waist circumference and flatter in others.
- There is evidence of heterogeneity by sex, so a single pooled straight-line effect can miss important structure.

## Repository contents

- `project.ipynb` — full analysis notebook
- `nhanes_2017_march2020.csv` — analysis dataset
- `readme_assets/` — figures displayed below

## Figure gallery

<table>
  <tr>
    <td><img src="readme_assets/figure_1.png" width="100%"></td>
    <td><img src="readme_assets/figure_2.png" width="100%"></td>
  </tr>
  <tr>
    <td align="center">Exploratory relationship between body-size measures and blood pressure.</td>
    <td align="center">Model-based comparison of fitted trends across candidate specifications.</td>
  </tr>
  <tr>
    <td><img src="readme_assets/figure_3.png" width="100%"></td>
    <td><img src="readme_assets/figure_4.png" width="100%"></td>
  </tr>
  <tr>
    <td align="center">Adjusted fitted curve for systolic blood pressure as waist circumference changes.</td>
    <td align="center">Subgroup comparison showing how the fitted association differs across groups.</td>
  </tr>
  <tr>
    <td><img src="readme_assets/figure_5.png" width="100%"></td>
    <td><img src="readme_assets/figure_6.png" width="100%"></td>
  </tr>
  <tr>
    <td align="center">Nonlinear fit highlighting curvature in the waist–SBP relationship.</td>
    <td align="center">Alternative adjusted view emphasizing uncertainty bands around fitted values.</td>
  </tr>
  <tr>
    <td><img src="readme_assets/figure_7.png" width="100%"></td>
    <td><img src="readme_assets/figure_8.png" width="100%"></td>
  </tr>
  <tr>
    <td align="center">Predicted mean SBP across waist circumference for one adjustment setting.</td>
    <td align="center">Comparison figure summarizing shape differences across sexes or covariate profiles.</td>
  </tr>
  <tr>
    <td><img src="readme_assets/figure_9.png" width="100%"></td>
    <td><img src="readme_assets/figure_10.png" width="100%"></td>
  </tr>
  <tr>
    <td align="center">Visualization of the fitted effect under a more flexible spline-based model.</td>
    <td align="center">Final comparison plot used to communicate the practical pattern in the data.</td>
  </tr>
</table>

## How to run

Open `project.ipynb` and run the notebook from top to bottom. The main Python packages used are:

- `pandas`
- `numpy`
- `matplotlib`
- `statsmodels`
- `patsy`

## Summary

This repository is a compact applied regression study on how abdominal body composition relates to systolic blood pressure in NHANES. The main statistical message is that the association is real, nonlinear, and better captured with flexible models than with a single straight-line effect.

## Reproducing the analysis

1. Install dependencies with `pip install -r requirements.txt`.
2. The raw NHANES files used in the project are already included under `data/nhanes/`.
3. Use `scripts/python/read.py` if you want to rebuild merged analysis tables from the raw files.
4. Open the notebooks in `notebooks/` for the main analysis workflows.
