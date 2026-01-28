# maize-et-yield-hybrid-model
Hybrid crop modeling + machine learning workflow for predicting **maize grain yield (GY)** and **seasonal evapotranspiration (ET)** in arid environments by coupling **DSSAT–CERES-Maize** with ML models (linear + tree-based + ensemble).
# ceres-maize-ml-hybrid

> **Portfolio / showcase repository**
> This repo documents the methodology and the implementation approach used in a peer-reviewed study.
> It is intentionally **not a fully runnable reproduction package** (DSSAT binaries, experimental inputs, and large simulation datasets are not redistributed here).

---

## What this project demonstrates

### 1) Process-based modeling (DSSAT CERES-Maize)
- CERES-Maize was calibrated and evaluated using multi-site field datasets, then used to produce long-term simulations that span wide combinations of environment × management.

### 2) Factorial simulation to generate large training data
- A full factorial design was used across **29 factor levels** (temperature, CO₂, radiation, cultivar, planting date/DOY, irrigation, compost, tillage) in **four sites** over **31 years (1990–2020)**, producing **>1.5 million simulated scenarios** of GY and ET.  
- R was used to automate “File X” editing and DSSAT runs across factorial levels.

### 3) ML models + hyperparameter optimization
- ML regressors trained to predict GY and ET from environmental + management inputs:
  - Linear Regression, Ridge, Lasso
  - KNN, Random Forest, XGBoost  
- Hyperparameter tuning via **Hyperopt** (Bayesian optimization approach) and evaluation on selected “warm” years.

### 4) Ensemble learning + interpretability
- A **Super Learner** ensemble stacks optimized base learners (out-of-fold predictions from k-fold CV).
- Feature importance analyzed with SHAP values (e.g., TreeExplainer for XGBoost).

---

## Associated publication

Attia, A., Govind, A., Qureshi, A.S., Feike, T., Rizk, M.S., Shabana, M.M.A., & Kheir, A.M.S. (2022).
**Coupling Process-Based Models and Machine Learning Algorithms for Predicting Yield and Evapotranspiration of Maize in Arid Environments.**
*Water*, 14(22), 3647. DOI: 10.3390/w14223647

Paper link:
https://www.mdpi.com/2073-4441/14/22/3647

Attia, A., El-Hendawy, S., Al-Suhaibani, N., Tahir, M.U., Mubushar, M., Vianna, M.S., Ullah, H., Mansour, E., Datta, A., 2021. **Sensitivity of the DSSAT model in simulating maize yield and soil carbon dynamics in arid Mediterranean climate: Effect of soil, genotype and crop management.** Field Crops Res. 260:107981. doi.org/10.1016/j.fcr.2020.107981


---

## Workflow summary (high level)

1. **Calibrate + evaluate CERES-Maize** on observed field datasets (multi-site, multi-cultivar).
2. **Generate factorial simulation dataset** (1990–2020):
   - perturb climate variables (Tmin/Tmax, CO₂),
   - vary management (cultivar RUE, planting date window, irrigation depletion trigger, compost rate, tillage),
   - run DSSAT for each scenario and extract seasonal GY + ET.
3. **Train ML models** on simulated data, test on selected hot years.
4. **Tune hyperparameters** using Hyperopt to minimize RMSE.
5. **Build Super Learner** by stacking optimized models.
6. **Explain models** with SHAP (global + local feature impact).

---

## Key “skills signal” (for hiring)
- Crop modeling: CERES-Maize calibration, evaluation, and scenario simulation design
- Data engineering: large factorial simulation management and feature table construction
- ML: model development (linear + tree), Bayesian hyperparameter optimization (Hyperopt)
- Ensembling: stacking / Super Learner with cross-validation
- Explainability: SHAP-based global & local feature importance

---

## What is intentionally NOT included
- DSSAT executables/binaries (install separately).
- Full experiment templates and site-specific proprietary inputs.
- The full generated 1.5M+ scenario dataset (size + reproducibility constraints).
- A turnkey “one command reproduces the paper” pipeline.

---

## References / tool links
- scikit-learn: https://scikit-learn.org/
- Hyperopt docs: https://hyperopt.github.io/hyperopt/
- SHAP docs (TreeExplainer): https://shap.readthedocs.io/en/latest/generated/shap.TreeExplainer.html
