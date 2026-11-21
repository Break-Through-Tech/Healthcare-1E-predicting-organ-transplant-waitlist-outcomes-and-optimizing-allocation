# Predicting Organ Transplant Wait List Outcomes and Optimizing Allocation

### 👥 **Team Members**

| Name                                                         | Contributions                                 |
|------------------------------------------------------------|-------------------------------------------------|
| [Naya Singhania](https://github.com/nayasinghania)         | Feature analysis, data pipeline, tree ensembles |
| [Jocelyn Lew](https://github.com/JocelynLew)               | Data normalization, logistic regression         |
| [Tracy Chen](https://github.com/TracyZexiChen)             | Data exploration, survival modelling            |
| [Maria Gonzalez](https://github.com/mariafernandagonzalez) | Feature engineering, survival modelling         |

---

## 🎯 **Project Highlights**

- Developed a machine learning model using `[model type/technique]` to address `[challenge project task]`.
- Achieved `[key metric or result]`, demonstrating `[value or impact]` for `[host company]`.
- Generated actionable insights to inform business decisions at `[host company or stakeholders]`.
- Implemented `[specific methodology]` to address industry constraints or expectations.

---

## 👩🏽‍💻 **Setup and Installation**

1. `git clone https://github.com/Break-Through-Tech/Healthcare-1E-predicting-organ-transplant-waitlist-outcomes-and-optimizing-allocation.git`

2. `pip install -r requirements.txt`

> If you are using a `venv`, after creating an activating the venv run `ipython kernel install --user --name=venv` to use your venv as the jupyter kernel.

> Sometimes, especially for Linux machines, additional system packages may need to be installed to allow functionality for certain Python packages.

> If you want GPU support for faster training of XGBoost models, create a file named `.env` at the project root and add `GPU=your-gpu-framework` (e.g. `GPU=cuda` for NVIDIA GPUs).

3. Run `jupyter lab` in the project root, and a window will pop up in your browser where you can run any of the notebooks.


---

## 🏗️ **Project Overview**

The company providing this challenge is MediMate foundation, a California 501(c)(3) nonprofit focused on improving healthcare outcomes through advanced analytics and predictive modeling. The challenge they have given us involves working on kidney transplant datasets to create models that can aid in effectively distributing available donated organs. 

This could be significant to the real world, as it would ensure that kidneys are matched to those who need and would benefit from it most. A doctor's expertise along with data-backed predictive modeling could create a better process for kidney donation recipients. 

Not only does this project have real-world potential, but it will give us the hard and soft skills needed to succeed in future ML jobs. This challenge project involves the entire pipeline from EDA to deployment and is built by a team much like what would be encountered in a real job.

---

## 📊 **Data Exploration**
- The OPTN Kidney Transplant Waitlist dataset was used, provided in a GZIP archive of 20.3 MB, containing 494,862 rows and 38 columns. 
- Data exploration and preprocessing approaches
- Insights from your Exploratory Data Analysis (EDA)
- Challenges and assumptions when working with the dataset(s)
- Plots, charts, heatmaps, feature visualizations, sample dataset images

---

## 🧠 **Model Development**

### Tree Ensembles
- We used XGBoost and Random Forest tree ensemble classification models to predict the class for column `event_adverse`, which determines if a kidney transplant candidate will experience an adverse event prior to transplantation.
- An 80/20 train test split was used with scaling to attempt to balance out class imbalance in the training set
- Across both models, `GridSearchCV` was used to efficiently experiment with a variety of hyperparameter combinations
- We utilized `GridSearchCV` cross-validation functionality with 5 folds to help prevent overfitting
- These models were evaluated on accuracy, precision, recall, F1 score, and ROC-AUC

### Logistic Regression
*Models Used*
- Logistic regression (scikit-learn) as an interpretable baseline, predicting death or removal as too sick within 365 days of listing.
- Splines for age and BMI, so their effects can be curved.
  
*Feature selection and hyperparameter tuning*
- Removed fields recorded after listing (`dialysis_started_after_listing`, `ON_DIALYSIS`, `A2A2B_ELIGIBILITY`) and replaced them with `on_dialysis_at_listing`.
- Added missing-value flags (cPRA, BMI), log dialysis time, two age interactions and prior listings; an ablation table measured each change separately.
- Tuned `C` (0.001 to 10) with 3-fold patient-grouped cross-validation on PR-AUC; `C` = 0.1 selected, with little difference across values.
  
*Training setup*
- Only patients with a full year of follow-up (listed by July 3, 2025).
- 80/20 train/test split grouped by patient: 353,804 train, 88,278 test; 1-year adverse rate about 3.9%.
- Metrics: ROC-AUC, PR-AUC, Brier score, top-decile lift, calibration and subgroup AUC.
- Baseline: v1 scored ROC-AUC 0.6925, partly from leaked fields; without them it is 0.6801, and the final model reaches 0.6822.

### Survival Modelling
- Model(s) used (e.g., CNN with transfer learning, regression models)
- Feature selection and Hyperparameter tuning strategies
- Training setup (e.g., % of data for training/validation, evaluation metric, baseline performance)

---

## 📈 **Results & Key Findings**

### Tree Ensembles
- Performance metrics (e.g., Accuracy, F1 score, RMSE)
- How your model performed
- Insights from evaluating model fairness
- Visualizations: Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

### Logistic Regression
- Performance metrics (e.g., Accuracy, F1 score, RMSE)
- How your model performed
- Insights from evaluating model fairness
- Visualizations: Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

### Survival Modelling
- Performance metrics (e.g., Accuracy, F1 score, RMSE)
- How your model performed
- Insights from evaluating model fairness
- Visualizations: Confusion matrix, precision-recall curve, feature importance plot, prediction distribution, outputs from fairness or explainability tools

---

## 🚀 **Next Steps**

### Model Limitations

### Logistic Regression
- The model sees only what's known on the day a patient joins the waitlist. It has no lab values, no other medical conditions and no updates after listing. This information limit capped ROC-AUC at about 0.68. Splines, interactions, tuning C and longer prediction windows didn't move it.
- Only 3.9% of patients have an adverse event within a year. The model sorts patients into risk levels well (observed risk rises from about 1% to 10% across risk deciles), but it can't pick out which individuals will have an event (PR-AUC 0.088, Brier skill about 2%).
- Patients transplanted within the year are labelled 0, so groups or regions that get transplanted faster look lower-risk. The region and race/ethnicity odds ratios can't be read as differences in clinical risk.
- The 1-year window misses most adverse events. For 2015 listings, 22.9% eventually had an adverse event but only 4.0% had one within a year. Listings from 2025–2026 are excluded because they don't have a full year of follow-up.
- BMI values outside 10–80 were replaced with the median. The two strongest risk signals are missing-data flags (`bmi_missing_or_invalid`, `functional_scale_unknown`), which likely mark incomplete records or patients too unwell to assess. They don't cause risk.
- The model ranks risk less well for ETHCAT 2 (AUC 0.637 vs 0.684–0.698 for other groups). Blood type AB has too few events (111) to know whether its lower AUC is real.

### What Would Be Done Differently

### Logistic Regression
- Check every feature for leakage before modelling. `dialysis_started_after_listing` and `ON_DIALYSIS` were recorded after listing, and they made up about 0.012 of the v1 ROC-AUC. A "known on listing day?" check for each column would have caught them early.
- Keep missing-value flags during preprocessing. Filling cPRA and BMI with the median hid which values were missing, and the raw file had to be reloaded to get that back.
- Do all preprocessing inside the training pipeline. The BMI median was computed on the full dataset before the split. It's a small effect, but imputation should be learned from training rows only, like scaling was.
- Set fairness targets and run subgroup checks up front. Report confidence intervals on the overall metrics too, and use repeated patient-grouped cross-validation instead of a single split.

### Additional Datasets / Techniques to Explore

### Logistic Regression
- Richer clinical data: (lab values, comorbidities such as diabetes, follow-up status updates) if available in the registry extract.
- Updating predictions over time: re-score patients at 3 or 6 months using post-listing data that is legitimately available by then.
---

## 🙏 **Acknowledgements**

Thank you to our challenge advisor and coach Beth Parnell for guiding us, supporting us, and keeping us on track in this project.

---

*This project is licensed under the [MIT License](https://github.com/Break-Through-Tech/Healthcare-1E-predicting-organ-transplant-waitlist-outcomes-and-optimizing-allocation/blob/main/LICENSE).*
