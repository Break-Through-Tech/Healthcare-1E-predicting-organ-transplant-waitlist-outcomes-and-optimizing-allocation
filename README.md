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
- `GridSearchCV` also allows for simple cross-validation, so we used 5 folds on each model
- These models were evaluated on accuracy, precision, recall, F1 score, and ROC-AUC

### Logistic Regression
- Model(s) used (e.g., CNN with transfer learning, regression models)
- Feature selection and Hyperparameter tuning strategies
- Training setup (e.g., % of data for training/validation, evaluation metric, baseline performance)

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

### What Would Be Done Differently

### Additional Datasets / Techniques to Explore

---

## 🙏 **Acknowledgements**

Thank your Challenge Advisor, host company representatives, TA, and others who supported your project.

---

*This project is licensed under the [name of license] License.*
