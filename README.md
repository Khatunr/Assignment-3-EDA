# Assignment 3: Exploratory Data Analysis (EDA)

## Project Overview
This project explores a cleaned lung cancer dataset to understand patient characteristics, examine how variables relate to the `Survival_Group` target, create additional features, and test basic feature-selection and dimensionality-reduction methods.

The target has two classes: `Short-Term` and `Long-Term` survival. The analysis is exploratory and does not establish causal relationships.

## Files
- `Assignment_3_EDA.ipynb` — notebook containing dataset overview, descriptive statistics, visualizations, correlation analysis, business insights, feature engineering, Variance Threshold, PCA, and reflection.
- `EDA_Report.pdf` — concise report summarizing the main findings.
- `cleaned_dataset_assignment3.csv` — updated dataset after feature engineering (include this file in the repository).
- `data/lung_cancer_cleaned.csv` — source cleaned dataset, if required by the notebook's relative path.

## Dataset
The notebook's recorded starting dataset contains 23,658 rows and 48 columns. The survival outcome is nearly balanced:
- Long-Term: 11,948 patients (50.50%)
- Short-Term: 11,710 patients (49.50%)

Selected descriptive statistics:
- Mean age: approximately 54.44 years (standard deviation 14.40).
- Mean tumor size: approximately 55.38 mm (standard deviation 26.00).
- Mean systolic blood pressure: approximately 134.46.
- Mean diastolic blood pressure: approximately 84.48.

## Feature Engineering
The notebook creates and visualizes five features:

1. **`Age_Group`** — groups age into 30–49, 50–64, and 65–79 categories. This makes it easier to compare survival distributions across age bands.
2. **`Tumor_Size_Group`** — groups tumor size into Small (up to 40 mm), Medium (40–70 mm), and Large (over 70 mm). This supports categorical comparisons of tumor size and survival.
3. **`Comorbidity_Count`** — sums seven yes/no comorbidity indicators. This gives a simple count of recorded comorbidities per patient.
4. **`Treatment_Count`** — sums three treatment indicator columns. It is intended as a compact summary of treatment indicators; its interpretation as a count of treatments depends on whether the underlying columns can be simultaneously active.
5. **`Blood_Pressure_Difference`** — calculates systolic blood pressure minus diastolic blood pressure, creating a single feature representing the difference between the two readings.

The notebook includes plots comparing each engineered feature with `Survival_Group`.

## EDA and Correlation Findings
The notebook contains more than 10 visualizations covering survival-group distribution, age, tumor size, performance status, cancer stage, treatment type, gender, smoking history, correlation patterns, and the five engineered features.

The outcome classes are balanced. Mean age and mean tumor size are very similar across survival groups. The correlation analysis found no predictor pairs exceeding an absolute Pearson correlation of 0.70 in the saved notebook output. Correlations between individual numeric predictors and the encoded survival target were small, so no single numeric predictor showed a strong linear relationship with the target.

### Business Insights
1. The survival target is balanced, with 50.50% Long-Term and 49.50% Short-Term patients.
2. Mean ages for Long-Term and Short-Term groups are approximately 54.5 and 54.4 years, respectively.
3. Mean tumor sizes are approximately 55.6 mm for Long-Term and 55.1 mm for Short-Term patients.
4. The stage visualization shows broadly similar outcome distributions across stages in this dataset; stage alone does not strongly separate the classes visually.
5. Individual numeric predictor correlations with the target are weak, suggesting that combined patterns may be more useful than relying on a single feature.

These are observations from this dataset, not clinical conclusions or evidence of causation.

## Variance Threshold and PCA
- **Variance Threshold:** Using a threshold of 0.01 retained all 50 predictors in the notebook output.
- **PCA:** The recorded analysis required 39 components to retain 90% of variance and 42 components to retain 95% of variance. Moving from 50 predictors to 39 components is a 22% reduction in feature count.
- **Logistic Regression comparison (values currently recorded in the saved notebook):**

| Approach | Number of features | Accuracy |
|---|---:|---:|
| Original features | 50 | 49.79% |
| PCA features (90% variance) | 39 | 49.64% |

The recorded accuracies are close to 50%, so this baseline model did not demonstrate strong predictive performance. PCA reduced the number of inputs with a small change in accuracy, but the transformed components are less directly interpretable.

## How to Run the Notebook
1. Clone or download this repository.
2. Ensure the notebook's input CSV is in the expected relative location. The original notebook reads `../data/lung_cancer_cleaned.csv`; either preserve that folder structure or update the path to match the repository.
3. Install the libraries used by the notebook if they are not already available, including `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`.
4. Open `Assignment_3_EDA.ipynb` in Jupyter Notebook, JupyterLab, or a compatible notebook environment.
5. Run the notebook cells from top to bottom. Confirm the final PCA comparison table and use those latest values in this README and PDF report.

## Limitations
This is an exploratory analysis and a basic baseline-model comparison. Correlation and visual patterns do not imply causation. More robust model evaluation, additional metrics, and further investigation would be needed before using the model for prediction.
