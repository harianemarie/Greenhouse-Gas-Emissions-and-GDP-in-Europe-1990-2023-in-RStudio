# Greenhouse Gas Emissions and GDP in Europe, 1990–2023

Does economic growth still come with more pollution? A panel of 29 European countries
over 34 years, built from two Eurostat series, taken from descriptive statistics through
to a two-way fixed effects regression.

The short answer the data gives: the apparent negative relationship between emissions and
GDP does not survive controls. Once country and year effects are included, it disappears.

## Data

| | Source | Measure |
|---|---|---|
| **X** — net GHG emissions | Eurostat `sdg_13_10` | chain-linked index, rebased to 2010 = 100 |
| **Y** — GDP at market prices | Eurostat `nama_10_gdp` | chained volume, index 2010 = 100 |

Merged on country and year. Unit of observation: the country-year pair.
**29 countries × 34 years = 858 observations.**

## Analysis

Density plots for both variables, summary statistics overall and by country, average
trends over time, and a side-by-side ranking of each country's change between 1990 and
2023.

Two contrasting countries are then followed individually: **France**, whose largely
nuclear energy mix and service-heavy economy let it grow while emissions fell, and
**Norway**, where GDP rose but emissions stayed high and began climbing again after 2013.
The pair makes the point that the growth–pollution link is not the same everywhere.

The relationship itself is plotted three ways: a linear fit, a quadratic fit testing the
environmental Kuznets curve, and a scatter of within-country annual changes.

## Results

| | Pooled OLS | Country FE | Country + Year FE |
|---|---|---|---|
| GHG emissions | −0.031\*\*\* | −0.042\*\*\* | 0.006 |
| | (0.011) | (0.013) | (0.007) |
| Country fixed effects | No | Yes | Yes |
| Year fixed effects | No | No | Yes |
| R² | 0.009 | 0.092 | 0.755 |
| Observations | 858 | 858 | 858 |

<sub>\*p<0.1; \*\*p<0.05; \*\*\*p<0.01</sub>

Without controls, emissions look mildly negatively associated with GDP, but they explain
under 1% of its variation. Adding country fixed effects strengthens the coefficient
slightly. Adding year effects as well kills it: the coefficient turns positive,
insignificant, and R² jumps to 0.755 — GDP variation is driven by common shocks and
structural country differences, not by emissions.

The quadratic fit shows no bell shape, so these data offer no support for a Kuznets
turning point over this period and this sample.

## Caveats

The GHG series is a **net** emissions measure rebased to an index. Countries with large
land-use sinks produce values that are negative or extreme once divided by a small base —
the sample minimum is −184.7 and the maximum 843.9, against a mean of 109.8. Those values
are not necessarily errors, but an index built on a near-zero denominator is unstable, and
the regression coefficients inherit that instability. Working in levels or in logs of
gross emissions would be the more defensible specification.

## Repository

```
ghg-gdp-europe/
├── analysis.R          # import, cleaning, figures, regressions
├── data/               # raw Eurostat extracts
├── figures/
└── report.pdf
```

R, with `ggplot2` for the figures and `stargazer` for the regression tables.

## Context

Final exam, *Introduction to Programming for Data Analysis* (E. Gallic) — Aix-Marseille
School of Economics, Master in Econometrics and Statistics (M1), 2025–2026. Individual
project.
