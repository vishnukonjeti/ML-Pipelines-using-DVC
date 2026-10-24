# ML Pipelines using DVC

An end-to-end Machine Learning pipeline for Twitter emotion detection (classifying text into *happiness* or *sadness*), modularized and versioned using [Data Version Control (DVC)](https://dvc.org/).

---

## 📁 Project Structure

```text
ML-Pipelines-using-DVC/
├── .gitignore
├── requirements.txt
├── dvc.yaml                      # Pipeline stages definition
├── notebook/
│   └── twitter_emotion_detection.ipynb  # Exploratory notebook
├── src/
│   ├── data_ingestion.py        # Fetches raw dataset & splits into train/test
│   ├── data_preprocessing.py    # Text cleaning, lemmatization, stop words removal
│   ├── feature_engineering.py   # Bag of Words (BoW) text vectorization
│   ├── model_building.py        # Model training (Gradient Boosting Classifier)
│   └── model_evaluation.py      # Evaluates metrics (Accuracy, Precision, Recall, AUC)
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd "ML Pipelines using DVC"
```

### 2. Create and activate a virtual environment
```bash
# Windows
python -m venv mlops
.\mlops\Scripts\activate

# Linux / macOS
python3 -m venv mlops
source mlops/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

---

## 🚀 Running the Pipeline

You can run individual pipeline stages manually:

```bash
# 1. Fetch & split data
python src/data_ingestion.py

# 2. Text preprocessing & cleaning
python src/data_preprocessing.py

# 3. Feature engineering (Bag of Words)
python src/feature_engineering.py

# 4. Train the model
python src/model_building.py

# 5. Evaluate the model (outputs metrics.json)
python src/model_evaluation.py
```

### Running with DVC
Initialize DVC and reproduce the pipeline:
```bash
dvc init
dvc repro
```

---

## 📊 Pipeline Stages

| Stage | Script | Input | Output |
|---|---|---|---|
| **Data Ingestion** | `src/data_ingestion.py` | Remote CSV URL | `data/raw/train.csv`, `data/raw/test.csv` |
| **Data Preprocessing** | `src/data_preprocessing.py` | `data/raw/` | `data/processed/train_processed.csv`, `data/processed/test_processed.csv` |
| **Feature Engineering** | `src/feature_engineering.py` | `data/processed/` | `data/features/train_bow.csv`, `data/features/test_bow.csv` |
| **Model Building** | `src/model_building.py` | `data/features/train_bow.csv` | `model.pkl` |
| **Model Evaluation** | `src/model_evaluation.py` | `data/features/test_bow.csv`, `model.pkl` | `metrics.json` |

---

## 📈 Evaluation Metrics

The model evaluation step generates a `metrics.json` containing:
- **Accuracy**
- **Precision**
- **Recall**
- **ROC-AUC**

