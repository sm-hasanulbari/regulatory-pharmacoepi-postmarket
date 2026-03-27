# Regulatory Pharmacoepidemiology — Post-Market Surveillance

## Rosiglitazone EMA Suspension 2010: A Natural Experiment

!\[Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
!\[Methods](https://img.shields.io/badge/Methods-ITS%20·%20DiD%20·%20IV%20·%20SCCS-orange)
!\[Data](https://img.shields.io/badge/Data-Synthetic%20GPRD--calibrated-green)
!\[Status](https://img.shields.io/badge/Status-Complete-brightgreen)

\---

## Research Question

> \\\*\\\*Did the EMA's 2010 suspension of rosiglitazone causally reduce MACE rates in European T2D patients? A natural experiment using interrupted time series, difference-in-differences, and instrumental variable analysis.\\\*\\\*

In September 2010, the European Medicines Agency suspended rosiglitazone (Avandia) following evidence of elevated cardiovascular risk — particularly myocardial infarction — first identified by Nissen \& Wolski (2007). This created a natural experiment: a sharp, externally imposed reduction in exposure that varied by region and prescriber, enabling causal estimation of the drug's cardiovascular impact using observational data.

This repository demonstrates the full pharmacoepidemiological toolkit used in post-authorisation safety studies (PASS) as required under EMA Pharmacovigilance Regulation 1235/2010.

\---

## Methods

|Method|Estimand|Reference|
|-|-|-|
|Interrupted Time Series (ITS)|Level and slope change at suspension|Bernal et al. (2017) Int J Epidemiol 46:348|
|Controlled ITS|ITS with pioglitazone as active comparator|Lopez Bernal et al. (2018) BMJ 362:k3444|
|Difference-in-Differences (DiD)|ATT — average treatment effect on treated|Angrist \& Pischke (2009)|
|Parallel Trends Test|DiD assumption validation|Rambachan \& Roth (2023) Rev Econ Stud|
|Instrumental Variable (IV) / 2SLS|LATE — local average treatment effect|Staiger \& Stock (1997) Econometrica 65:557|
|Self-Controlled Case Series (SCCS)|IRR — eliminates time-invariant confounding|Maclure (1991) Epidemiology 2:174|
|Joinpoint Regression|Structural break detection in MACE trend|Kim et al. (2000) Stat Med 19:335|
|PASS Design Simulation|Sample size and power for regulatory studies|EMA Reg 1235/2010; Schoenfeld (1981)|

\---

## Data

Synthetic time-series cohort (N=50,000 T2D patients, 52 quarters: 2004 Q1–2016 Q4) calibrated to:

* Nissen \& Wolski (2007) NEJM 356:2457 — OR 1.43 for MI
* Graham et al. (2010) JAMA 304:411 — post-market surveillance findings
* EMA (2010) EPAR Avandia EMA/357949/2010 — suspension assessment
* Juurlink et al. (2009) BMJ 339:b2701 — real-world prescribing data

\---

## Results Summary

|Metric|Value|
|-|-|
|Total person-quarters|*2,600,000*|
|Pre-suspension MACE (rosiglitazone)|*from kpi.csv*|
|ITS level change (β₂)|*−3.353 (p<0.0001)*|
|DiD coefficient|*−3.412 (p<0.0001)*|
|IV first-stage F-statistic|*37.9 (strong instrument)*|
|SCCS observed IRR|*1.262*|
|SCCS calibration target IRR|1.43|

\---

## Figures

|Figure|Description|
|-|-|
|`pharmacoepi\\\_fig1\\\_rates.png`|Prescription rates and MACE trends 2004–2016|
|`pharmacoepi\\\_fig2\\\_its.png`|ITS segmented regression with counterfactual projection|
|`pharmacoepi\\\_fig3\\\_did.png`|DiD means plot and parallel trends test|
|`pharmacoepi\\\_fig4\\\_iv.png`|IV first and second stage diagnostics|
|`pharmacoepi\\\_fig5\\\_sccs.png`|SCCS exposure windows and cross-method IRR comparison|
|`pharmacoepi\\\_fig6\\\_pass.png`|PASS power curves and minimum sample size|
|`pharmacoepi\\\_fig7\\\_joinpoint\\\_comparison.png`|Joinpoint regression and cross-method comparison|

\---

## Repository Structure

```
regulatory-pharmacoepi-postmarket/
├── python/
│   ├── pharmacoepi\\\_postmarket.ipynb     # Main notebook (10 cells)
│   ├── pharmacoepi\\\_timeseries.csv       # Quarterly cohort data
│   ├── pharmacoepi\\\_its\\\_results.csv      # ITS regression coefficients
│   ├── pharmacoepi\\\_did\\\_results.csv      # DiD estimates
│   ├── pharmacoepi\\\_iv\\\_results.csv       # IV/2SLS results
│   ├── pharmacoepi\\\_sccs\\\_results.csv     # SCCS IRR summary
│   ├── pharmacoepi\\\_sccs\\\_windows.csv     # SCCS window-level data
│   ├── pharmacoepi\\\_pass\\\_design.csv      # Full PASS power grid
│   ├── pharmacoepi\\\_pass\\\_min\\\_n.csv       # Minimum N by follow-up
│   ├── pharmacoepi\\\_joinpoint.csv        # Joinpoint fitted values
│   └── pharmacoepi\\\_kpi.csv             # Summary KPIs
├── requirements.txt
└── README.md
```

\---

## Setup \& Usage

```bash
git clone https://github.com/sm-hasanulbari/regulatory-pharmacoepi-postmarket.git
cd regulatory-pharmacoepi-postmarket
pip install -r requirements.txt
jupyter notebook python/pharmacoepi\\\_postmarket.ipynb
```

Run cells in order. All data is generated synthetically in Cell 2 — no external downloads required. Total runtime \~2 minutes.

\---

## Relevance to EDICT MSCA Doctoral Network

This project directly addresses **Project 10 (University of Utrecht)** — regulatory RWE and post-authorisation safety studies:

|Project 10 Requirement|Demonstrated Here|
|-|-|
|PASS study design|Power simulation, min N, EMA Reg 1235/2010 alignment|
|Regulatory RWE methods|ITS, DiD, IV — all standard pharmacovigilance tools|
|EMA regulatory process|Rosiglitazone EPAR, suspension timeline, enforcement variation|
|Causal inference from claims data|SCCS eliminates time-invariant confounding|
|Pharmacoepidemiology pipeline|Full synthetic GPRD-calibrated cohort|
|Cross-method triangulation|4 methods compared on same data — consistency check|

\---

## References

|Reference|Role|
|-|-|
|Nissen \& Wolski (2007) NEJM 356:2457. PMID 17517853|Original safety signal — OR 1.43 calibration target|
|EMA (2010) EPAR Avandia. EMA/357949/2010|Suspension decision and rationale|
|Graham et al. (2010) JAMA 304:411. PMID 20639564|Post-market MACE rates|
|Bernal et al. (2017) Int J Epidemiol 46:348. PMID 27283160|ITS methods|
|Angrist \& Pischke (2009) Mostly Harmless Econometrics|DiD and IV|
|Staiger \& Stock (1997) Econometrica 65:557|IV relevance — F > 10|
|Maclure (1991) Epidemiology 2:174. PMID 2021087|SCCS design|
|Farrington (1995) Stat Med 14:1433. PMID 7481194|SCCS conditional Poisson|
|Schoenfeld (1981) Biometrika 68:316|Log-rank power approximation|
|Kim et al. (2000) Stat Med 19:335. PMID 10649302|Joinpoint regression|
|Rambachan \& Roth (2023) Rev Econ Stud|Parallel trends sensitivity|
|EMA Reg 1235/2010|PASS regulatory framework|

\---

## Author

**Sm Hasan ul Bari** — MBBS · MSc Advanced Biostatistics \& Epidemiology (Erasmus Mundus, Distinction) · MSc Health Economics \& Decision Modelling (Sheffield, Merit)  
Associate HTA Analyst, NICE Manchester · Technical Consultant, UNICEF NYC  
[github.com/sm-hasanulbari](https://github.com/sm-hasanulbari) · [ORCID: 0000-0002-5209-2029](https://orcid.org/0000-0002-5209-2029)

