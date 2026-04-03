<div align="center">
 
```
 ___                  ___               
/ __|_ __  __ _ _ __ / __| __ __ _ _ _  
\__ \ '_ \/ _` | '  \\__ \/ _/ _` | ' \ 
|___/ .__/\__,_|_|_|_|___/\__\__,_|_||_|
    |_|                                 
```
 
**ML-powered email spam detection trained on the Enron dataset.**
 
![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![TF-IDF](https://img.shields.io/badge/TF--IDF-Vectorizer-blueviolet?style=flat-square)
![LinearSVC](https://img.shields.io/badge/LinearSVC-Classifier-blue?style=flat-square)
 
</div>
 
---

## What is this?
 
**SpamScan** is a machine learning pipeline that classifies emails as **spam** or **ham** using a TF-IDF vectorizer paired with a calibrated LinearSVC classifier — trained on the real-world Enron email corpus.
 
It cleans raw email text, extracts bigram features, trains a high-accuracy SVM model, and lets you test any message via a simple CLI. The model is saved as a `.joblib` file and can be loaded for inference without retraining.
 
---
 
## Model Details
 
| | Detail |
|---|---|
| **Dataset** | Enron Email Dataset (public) |
| **Algorithm** | LinearSVC with probability calibration |
| **Features** | TF-IDF unigrams + bigrams |
| **Test Split** | 27% holdout |
| **Threshold** | 0.80 spam confidence (adjustable) |
| **Output** | Label + spam probability + confidence score |
 
---
 
## Results
 
```
Accuracy : ~98%
 
              precision    recall  f1-score
Ham               0.99      0.98      0.99
Spam              0.97      0.98      0.97
```
 
> Results may vary slightly depending on the version of the Enron CSV used.
 
---

## Dataset Setup
 
This project uses the **Enron Email Dataset**.

Once downloaded, place the file here:
 
```
data/Enron.csv
```
 
The CSV must have these columns: `subject`, `body`, `label` (0 = ham, 1 = spam).
 
---
 
## Getting Started
 
```bash
# Clone the repo
git clone https://github.com/Ree2612/spam-detector.git
cd spam-detector
 
# Install dependencies
pip install -r requirements.txt
 
# Add your dataset (see Dataset Setup above)
# Then train the model
# Run CLI predictions
python predict.py
```

---
 
## How It Works
 
```
Raw email (subject + body)
        │
        ▼
  Text cleaning
  - lowercase
  - remove URLs → replace with "url"
  - strip special characters
        │
        ▼
  TF-IDF Vectorizer
  - unigrams + bigrams
  - stop words removed
  - max_df=0.95, min_df=3
        │
        ▼
  LinearSVC Classifier
        │
        ▼
  CalibratedClassifierCV
  (converts SVC scores → probabilities)
        │
        ▼
  Threshold check (default: 0.80)
        │
   ┌────┴────┐
   │  SPAM   │  spam_prob >= 0.80
   │   HAM   │  spam_prob <  0.80
   └─────────┘
```
 
---

## Preview 
CODE SNIPPETS:
<img width="2106" height="1233" alt="Screenshot 2026-04-03 190326" src="https://github.com/user-attachments/assets/a0d9ae33-4f2e-4bd7-a8d2-82b893259e50" />
<img width="1736" height="1121" alt="Screenshot 2026-04-03 190446" src="https://github.com/user-attachments/assets/322550f4-4269-4c47-8377-e91ec74398c5" />
<img width="1666" height="1421" alt="Screenshot 2026-04-03 190623" src="https://github.com/user-attachments/assets/efdcdbf0-b881-4dae-b741-3c65c48a7484" />
<img width="2241" height="1243" alt="Screenshot 2026-04-03 190643" src="https://github.com/user-attachments/assets/d3982dd8-53b5-4207-81ac-cb295b245a87" />
