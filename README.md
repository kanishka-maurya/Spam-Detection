# 🚀 ML Project Pipeline with DVC & Experiment Tracking

This project demonstrates how to build a **modular**, **reproducible**, and **experiment-trackable** machine learning pipeline using **Git**, **DVC**, and **DVCLive**.

---

## 📌 What This Project Does

### 1️⃣ Organized Project Structure

- Set up a well-structured codebase with a `src/` directory containing modular components for:
  - Data preprocessing
  - Model training
  - Model evaluation

- Created dedicated directories for:
  - `data/` → raw and processed datasets  
  - `models/` → trained model artifacts  
  - `reports/` → evaluation metrics, logs, and plots  

> ✅ These folders are excluded from version control to keep the repository lightweight and clean.

---

### 2️⃣ DVC Pipeline (Without Parameters)

- Initialized **DVC (Data Version Control)** to track data and automate pipeline stages.
- Created a `dvc.yaml` file to define pipeline stages:
  - Preprocessing
  - Training
  - Evaluation

Each stage is connected to its inputs (scripts/data), outputs (artifacts), and dependencies.

- Verified pipeline flow using:
  ```bash
  dvc repro
  dvc dag

---

### 3️⃣ DVC Pipeline with Parameters

- Added a `params.yaml` file to store configurable hyperparameters.

---

### 4️⃣ Experiment Tracking with DVCLive

Installed and integrated **DVCLive**, a lightweight tool for experiment tracking.

In the model training script:

✅ Logged key performance metrics:
- **Accuracy**
- **Precision**
- **Recall**

✅ Logged all training hyperparameters from `params.yaml`.

✅ Used the `Live` context manager to automatically save metrics and parameters for each experiment:

```python
from dvclive import Live
from sklearn.metrics import accuracy_score, precision_score, recall_score

with Live(save_dvc_exp=True) as live:
    live.log_metric("accuracy", accuracy_score(y_test, y_pred))
    live.log_metric("precision", precision_score(y_test, y_pred))
    live.log_metric("recall", recall_score(y_test, y_pred))
    live.log_params(params)


