# Online Game Network Protocol Classification

This project explores network packet metadata captured while an online game is running and compares machine learning models for predicting each packet's network protocol.

## Project contents

- `Copy of Online_game.ipynb` — Google Colab notebook with data inspection, cleaning, visualizations, model training, evaluation, and an example prediction.
- `merged_battleground.csv` — input dataset expected by the notebook. It is not included here; provide your own copy of this file.

## Dataset

The notebook expects a CSV named `merged_battleground.csv` with at least these columns:

- `Time` — packet timestamp
- `Length` — packet length
- `Protocol` — protocol label to predict

The sample rows shown in the notebook also include `No.`, `Source`, `Destination`, and `Info`. The model uses only packet length and time-derived features (`Hour`, `Minute`, and `Second`); it does not use the source/destination addresses or packet description.

## Requirements

- Python 3
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn

The notebook installs these packages in its first cell. If running locally, install them with:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn
```

## Run the notebook

1. Open the notebook in Google Colab or Jupyter.
2. Make `merged_battleground.csv` available at the path expected by the notebook. The current code uses `/content/merged_battleground.csv`, which is a Google Colab path; update `file_path` when running elsewhere.
3. Run the notebook cells in order.

The notebook inspects and cleans the data, limits it to 100,000 rows when needed, extracts time features, and compares Logistic Regression, K-Nearest Neighbors, Decision Tree, and Random Forest classifiers. It reports accuracy and per-class metrics and plots a confusion matrix for the best model. It also demonstrates a prediction for one example packet and displays Random Forest feature importance.

## Notebook completion note

The supplied notebook references `label_encoder`, `X_train`, `X_test`, `y_train`, and `y_test` in its model-training cells, but does not include the code that creates them. Add a preprocessing and train/test-split cell before the scaling/training cells. That step should encode `Protocol`, split the features and labels into training and test sets (ideally with stratification), and define the variables above. Until then, running the notebook from top to bottom will stop with an undefined-variable error.

## Scope and limitations

This is an educational classification experiment using packet metadata. Its reported performance depends on the supplied dataset and split. Because the current features are limited to packet length and time of day, results should not be treated as a general-purpose network traffic classifier or a security assessment.
