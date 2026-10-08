# In-Hospital Mortality Prediction

An individual University of Melbourne coursework project (COMP90089), September–November 2025, comparing linear-activation and ReLU multilayer perceptrons for patients with severe hypotension.

## Contribution
I completed this individual project, including data preparation, model training and testing, data analysis and visualisation.

## Workflow
- Explore age, gender, APS III and Charlson comorbidity index distributions.
- Construct the coursework mortality label as `dod.notna()`: 1 indicates in-hospital mortality under the assignment definition, and 0 indicates its absence.
- Stratified 80/20 split: 4,084 training and 1,022 test records.
- Fit numerical mean imputation and standardisation, plus categorical one-hot encoding, within a scikit-learn pipeline. Input features in the supplied dataset had no missing values.
- Tune an identity-activation MLP using five-fold cross-validation over 27 configurations, selecting by accuracy.
- Compare a ReLU MLP using the selected architecture and learning rate; ReLU was not separately tuned.
- Visualise feature distributions, tuning heatmaps and confusion matrices.

## Recorded results
These are aggregate outputs saved in the original coursework notebook, not a fresh training run.

| Metric | Identity activation | ReLU |
|---|---:|---:|
| Test accuracy | 0.6614 | 0.6526 |
| Precision | 0.6883 | 0.6751 |
| Recall | 0.8680 | 0.8892 |
| F1 | 0.7678 | 0.7675 |

Best identity configuration: one hidden layer of 16 neurons, learning rate 0.001. Positive class: mortality. The test-set majority-class accuracy baseline is approximately 64.5%. ReLU increases recall at the expense of precision; the comparison does not establish that the underlying relationships are linear.

## Evaluation notes

- The dataset contains 5,106 records; only age, gender, APS III and Charlson comorbidity index are used as predictors. The outcome field is not included among the inputs.
- Hyperparameter selection uses training-set cross-validation accuracy. Precision, recall and F1 are reported on the held-out test set for the positive mortality class.
- The ReLU model reuses the identity model's selected configuration rather than receiving an independent hyperparameter search.
- Reported differences are descriptive results from one train/test split, without uncertainty intervals or external validation.
- Probability calibration and clinical decision thresholds were not evaluated. These results do not establish clinical usefulness.

## Run locally
Install dependencies with `pip install -r requirements.txt`, then open `assignment2.ipynb` in Jupyter and run cells in order. A separately authorised local copy of `hypotension_patients.csv` must be placed beside the notebook. Required columns: `anchor_age`, `gender`, `dod`, `apsiii`, `charlson_comorbidity_index`.

## Data provenance and acknowledgement

The analysis uses the local file `hypotension_patients.csv` supplied with the project materials. Those materials do not identify the original dataset creators, database version or redistribution licence. The original source citation and applicable terms therefore remain to be confirmed; no specific database attribution is inferred from column names.

My contribution is the analysis and modelling workflow, not creation of the underlying patient dataset. Patient-level records are not included in this repository. To reproduce the analysis, obtain an authorised copy from the original provider and follow its access and citation requirements.

## Repository scope
Patient-level data are deliberately not distributed. The notebook has been exported without saved outputs or identifying metadata. Original model code is retained; explanatory findings are consolidated here to avoid overstated conclusions in the original notebook. No model was retrained for this repository preparation. This is an educational model comparison, not a clinically validated prediction system.
