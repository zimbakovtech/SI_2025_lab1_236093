# 🎾 Tennis Match Prediction

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
[![Python Version](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)

Predict ATP tennis match outcomes with advanced machine learning on 2015–2024 data.

---

## 📋 Table of Contents

1. [Overview](#overview)  
2. [Key Features](#key-features)  
3. [Repository Structure](#repository-structure)  
4. [Installation & Setup](#installation--setup)  
5. [Data Preparation](#data-preparation)  
6. [Training & Evaluation](#training--evaluation)  
7. [Results & Metrics](#results--metrics)  
8. [Usage](#usage)  
9. [Future Work](#future-work)  
10. [License](#license)

---

## 🔍 Overview

This project builds, trains, and evaluates multiple classifiers to predict the winners of ATP tennis matches. Based on Jeff Sackmann’s publicly available match data from 2015 to 2024, we engineer rich features—Elo ratings, head‑to‑head stats, recent form metrics—and compare model performances.

---

## 🚀 Key Features

- **Data Ingestion & Cleaning**  
  Load and combine raw CSVs, filter for main‑draw matches, normalize surfaces, and handle missing entries.

- **Feature Engineering**  
  - **Elo Ratings**: Global & surface‑specific, updated pre‑match with K = 32  
  - **Head‑to‑Head**: Win–loss differential for player rivalries  
  - **Recent Form**: Rolling statistics over last N matches (aces, double faults, break points saved)  
  - **Ranking Metrics**: Differences in ATP rank and ranking points  
  - **Tournament Encoding**: Importance level and round information  

- **Modeling Suite**  
  - Naive Bayes  
  - Decision Tree  
  - Random Forest  
  - XGBoost (top performer)  
  - CatBoost  
  - LightGBM  
  - Neural Network  

- **Evaluation Tools**  
  Calculate accuracy, AUC‑ROC, confusion matrices, and feature importances.

- **Prediction Utility**  
  Interactive script to load a trained model and forecast match outcomes by player IDs, surface, and date.

---

## 📁 Repository Structure

```
TennisPrediction/
├── data/
│   ├── raw/                 # Raw match CSVs (2015–2024)
│   ├── processed/           # Cleaned & engineered datasets
│   └── players/             # Precomputed Elo ratings
│
├── src/
│   ├── feature_engineering/ # Elo, stats, head2head
│   ├── functions/           # Preprocessing utilities
│   ├── models/              # Individual model definitions
│   ├── train_models.py      # Training and evaluation pipeline
│   └── processing_data.py   # Data preparation pipeline
│
├── requirements.txt  
├── LICENSE  
└── README.md
```

---

## ⚙️ Installation & Setup

1. **Clone the repo**  
   ```bash
   git clone https://github.com/zimbakovtech/TennisPrediction.git
   cd TennisPrediction
   ```

2. **Create & activate a virtual environment**  
   ```bash
   python3 -m venv venv
   source venv/bin/activate    # macOS/Linux
   venv\Scripts\activate     # Windows
   ```

3. **Install dependencies**  
   ```bash
   pip install -r requirements.txt
   ```

---

## 🗄️ Data Preparation

Run the data pipeline to generate the final dataset:
```bash
python src/processing_data.py
```
This script:
- Merges raw files  
- Encodes categorical features (rounds, surfaces, etc.)  
- Computes difference metrics (`rank_diff`, `points_diff`, `ace_diff`, etc.)  
- Mirrors matches for bidirectional modeling  
- Calculates pre‑match Elo ratings

---

## 🏋️‍♂️ Training & Evaluation

Train and evaluate models with a 70/30 train-test split:
```bash
python src/train_models.py
```
Outputs:
- Performance metrics for each classifier  
- Confusion matrices and ROC curves  
- Feature importance rankings

---

## 📊 Results & Metrics

**XGBoost** achieved the best test accuracy of **66.30%** (67.76% train)  
A concise comparison:

| Model             | Test Acc. | Train Acc. |
|-------------------|----------:|-----------:|
| Naive Bayes       |    64.54% |     65.29% |
| Decision Tree     |    64.07% |     65.64% |
| Random Forest     |    65.26% |     66.97% |
| **XGBoost**       | **66.30%**| **67.76%** |
| CatBoost          |    65.63% |     66.26% |
| LightGBM          |    66.11% |     68.12% |
| Neural Network    |    65.72% |     66.36% |

---

## 🎯 Usage

1. **Predict a Match**  
   ```bash
   python predict.py      --player1_id 1045      --player2_id 2023      --surface Hard      --date 2025-01-20
   ```
2. **Visualize Results**  
   Load saved evaluation plots in the `outputs/` directory.

---

## 📅 Future Work

- Develop a REST API (Flask/FastAPI) for live predictions  
- Build a web dashboard with React or static HTML  
- Automate weekly data ingestion  
- Integrate new features (injury flags, travel distances)  
- Implement periodic retraining to address concept drift

---

## 📄 License

This project is licensed under the MIT License.  
See the [LICENSE](LICENSE) file for details.

*Prepared by Damjan Zimbakov & Andrej Milevski — June 2025*
