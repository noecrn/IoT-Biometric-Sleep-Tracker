# 💤 MMASH Sleep Detector

## 🎯 Objective

Build a sleep detection model using multimodal data: heart rate (RR), movement (actigraphy), and sleep annotations.

## 🧠 What it does

* Preprocesses raw RR and actigraphy signals.
* Extracts windowed statistical features.
* Labels sleep intervals using `sleep.csv`.
* Trains a classifier to predict sleep windows.
* Evaluates and visualizes model performance.

## 🗂️ Project Structure

```
├── data/
│   ├── raw/             # Original MMASH files (not committed)
│   ├── processed/       # Merged per-user data
│   └── features/        # Extracted feature windows with labels
├── notebooks/           # EDA, model training, evaluation
├── reports/
│   └── figures/         # Generated plots for README & reports
├── src/
│   └── data/            # Preprocessing and loading logic
├── prepare_all.py       # Run full pipeline
├── main.py              # Entry point for model training/testing
├── requirements.txt     # Python deps
└── Makefile             # Run clean/train/eval commands
```

## 🚀 Getting Started

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## 🧰 Usage

```bash
make prepare     # Preprocess and generate features
make train       # Train model on all users
make eval        # Evaluate model
make train_final # Final model training and scaling
```

## 📊 Final Results

After several iterations of feature engineering and model tuning, the final model is a **Tuned XGBoost Classifier**. It achieves the following performance on the hold-out test set:

**Classification Report (Sleep Detection)**
```
              precision    recall  f1-score   support

   False           0.99      0.93      0.96      4893
    True           0.76      0.95      0.85      1182

accuracy                               0.93      6075

macro avg          0.87      0.94      0.90      6075
weighted avg       0.94      0.93      0.94      6075
```

## 💡 Key Findings

The most significant performance improvement did not come from hyperparameter tuning, but from **feature engineering**. The addition of **rolling statistics** (e.g., mean and standard deviation of heart rate and activity over 5 and 15-minute windows) was the key factor in boosting the F1-score for sleep detection from ~0.76 to **0.85**.

## 📎 Notes

* Raw data excluded from git (`data/raw/`).
* Processed and feature data auto-generated.

## 🤝 Acknowledgements

Data from [MMASH dataset](https://physionet.org/content/mmash/1.0.0/)

## 📬 Contact

Noé Cornu • [noe.cornu@epita.fr](mailto:noe.cornu@epita.fr) • [GitHub](https://github.com/noecrm)
