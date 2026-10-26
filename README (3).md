# Blood-Brain Barrier Penetration Prediction

Predict whether a compound penetrates the blood-brain barrier, from its structure alone, using Morgan fingerprints.

Author: Masood Ur Rehman, MSc Drug Discovery and Development, Uppsala University

## Dataset
MoleculeNet BBBP, 2,050 compounds, 1,567 penetrant and 483 non-penetrant.
After dropping invalid SMILES, 2,039 compounds remained.
Source: https://deepchemdata.s3-us-west-1.amazonaws.com/datasets/BBBP.csv

## Method
- 1,024-bit Morgan fingerprints, radius 2, with RDKit
- Stratified 80/20 train/test split, random_state 42
  - Train: 1,631, Test: 408
- Models: Random Forest (300 trees), SVM (RBF), kNN (k=5), and a small neural network MLP (128, 64)

## Results
| Model | Accuracy | AUC |
|---|---|---|
| Random Forest | 0.892 | 0.929 |
| SVM | 0.909 | 0.906 |
| kNN | 0.885 | 0.847 |
| Neural network MLP | 0.875 | 0.891 |

Random Forest 5-fold cross-validation AUC: mean 0.868
(0.773, 0.822, 0.800, 0.958, 0.985)

## Honest notes
- The neural network did not beat the classic models.
- Class 0 recall was low for all models (0.54 to 0.64), because the data is imbalanced.
- Permutation importance showed no single fingerprint bit dominates; the top bit was 357 at 0.0076.

## Files
- bbbp_prediction.ipynb: full workflow in Google Colab
- bbbp_results.csv: model comparison table

## Tools
Python, RDKit, pandas, scikit-learn, Google Colab

Educational project. Not a chemical safety assessment, and not proof that a drug reaches the brain.
