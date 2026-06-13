
# COVID-19 Data Analysis & Epidemic Modelling

## Overview
A comprehensive analysis of the COVID-19 pandemic combining real-world data exploration, mathematical epidemic modelling, and machine learning forecasting. Built as part of a self-directed summer learning project, 2026.

## Project Structure
covid-epidemic-modelling/
├── notebooks/
│   ├── 01_data_exploration.ipynb      # Multi-country COVID data analysis
│   ├── 02_seir_model.ipynb            # SEIR epidemic model from scratch
│   ├── 03_model_fitting.ipynb         # Fitting model to real UK data
│   └── 04_ml_forecasting.ipynb        # Random Forest 14-day forecasting
├── figures/                           # Saved plots
├── data/                              # Raw and processed datasets
└── README.md

## Tools & Libraries
- Python, NumPy, Pandas
- Matplotlib, Seaborn
- Scikit-learn (Random Forest)
- SciPy (ODE solving, curve fitting)

## Part 1 — Data Exploration
Analysed real COVID-19 data from Our World in Data across 5 countries 
(UK, US, India, Brazil, Germany).

**Key findings:**
- Raw death counts are misleading — India appeared worst but had the lowest 
  deaths per capita due to its younger population
- The 2022 Omicron wave caused the largest case spike despite lower mortality, 
  reflecting high transmissibility but reduced severity
- Clear decoupling of cases and deaths post-vaccination, providing real-world 
  evidence of vaccine effectiveness

## Part 2 — SEIR Epidemic Model
Implemented the SEIR (Susceptible-Exposed-Infectious-Recovered) model from scratch 
using Euler's method, then validated against scipy's odeint solver.

**Model equations:**
- dS/dt = -βSI/N
- dE/dt = βSI/N - σE  
- dI/dt = σE - γI
- dR/dt = γI

**Key findings:**
- With R0=3 (β=0.3, γ=0.1), ~94% of a population of 67 million eventually infected
- Vaccination rate v=0.01 sufficient to suppress epidemic entirely
- Euler method and odeint produced near-identical results, validating implementation

## Part 3 — Fitting Model to Real Data
Fitted a two-phase SEIR model to UK first wave data (March-June 2020) using 
scipy's curve_fit, explicitly modelling the lockdown on 23rd March 2020.

**Key findings:**
- Pre-lockdown R0: ~7.6 (high but uncertain due to sparse pre-lockdown data)
- Post-lockdown R0: ~1.06 (barely above 1, consistent with slow growth under lockdown)
- Single-phase models fail to capture policy interventions — time-varying β essential

## Part 4 — Machine Learning Forecasting
Built a Random Forest model to forecast UK cases 14 days ahead using lag features 
(past 14 days of case data).

**Key findings:**
- MAE: 764 cases/day on test set
- Most important features: lag_1 (yesterday) and lag_14 (two weeks ago)
- Model struggled with distribution shift — trained on pandemic waves, tested on 
  quiet endemic period

## SEIR vs ML Comparison

| Aspect | SEIR Model | Random Forest |
|---|---|---|
| Approach | Mechanistic | Data-driven |
| Interpretability | High | Low |
| Handles interventions | Poorly | Implicitly |
| Best use case | Policy simulation | Short-term forecasting |

## Limitations
- SEIR assumes homogeneous mixing — real populations have complex contact structures
- Two-phase model still oversimplifies — lockdown compliance increased gradually
- ML model trained on pandemic period performs poorly on endemic period
- Case data quality varies significantly between countries

## Author
Ella — First year Mathematics student, University of Bath  
Summer 2026 placement preparation project