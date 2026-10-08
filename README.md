# In-Hospital Mortality Prediction

An individual University of Melbourne coursework project (COMP90089), September–November 2025, comparing linear-activation and ReLU multilayer perceptrons for patients with severe hypotension.

## Contribution
Wenrui Chen completed this individual project, including data preparation, model training and testing, data analysis and visualisation.

## Workflow
- Explore age, gender, APS III and Charlson comorbidity index distributions.
- Construct the mortality label from non-missing `dod`, confirmed by the project owner as the coursework definition of in-hospital mortality.
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

## Run locally
Install dependencies with `pip install -r requirements.txt`, then open `assignment2.ipynb` in Jupyter and run cells in order. A separately authorised local copy of `hypotension_patients.csv` must be placed beside the notebook. Required columns: `anchor_age`, `gender`, `dod`, `apsiii`, `charlson_comorbidity_index`.

## Data and scope
Patient-level data are deliberately not distributed. The notebook has been exported without saved outputs or identifying metadata. Original model code is retained; explanatory findings are consolidated here to avoid overstated conclusions in the original notebook. No model was retrained for this repository preparation. This is an educational model comparison, not a clinically validated prediction system.
