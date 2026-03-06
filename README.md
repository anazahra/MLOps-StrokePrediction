# 🦠 MLOps-StrokePrediction

[![Python 3.11](https://img.shields.io/badge/Python-3.11-blue?logo=python)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![MLflow](https://img.shields.io/badge/MLflow-Tracking-orange?logo=mlflow)](https://mlflow.org)
[![Open in Codespaces](https://img.shields.io/badge/GitHub-Codespaces-green?logo=github)](https://codespaces.new/anazahra/MLOps-StrokePrediction)

> Pipeline MLOps semi-otomatis untuk prediksi risiko stroke menggunakan
> Random Forest dengan tracking eksperimen via MLflow dan versioning data via DVC.

## 🎯 Tujuan Proyek

Stroke merupakan penyebab kematian kedua terbesar secara global. Deteksi dini
adalah kunci penanganan. Proyek ini membangun sistem prediksi risiko stroke
berbasis MLOps yang dapat:

- Memprediksi risiko stroke dalam < 2 menit per pasien
- Melakukan retraining berkala saat performa turun atau data drift terdeteksi
- Melacak semua eksperimen dan versi model secara sistematis

**Target Metrik:**
| Metrik | Target | Alasan |
|--------|--------|--------|
| Recall | >= 80% | Minimasi false negative (pasien stroke tidak terdeteksi) |
| F1-Score | >= 75% | Keseimbangan precision-recall pada data imbalanced |
| AUC-ROC | >= 0.85 | Kemampuan diskriminasi kelas |

## 📂 Dataset

- **Sumber:** [Stroke Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset) (Kaggle, fedesoriano 2021)
- **Jumlah:** 5.110 records, 12 fitur klinis & demografis
- **Target:** `stroke` (biner, highly imbalanced: 4,9% positif)
- **Challenge:** Missing values pada BMI (201 baris), class imbalance ekstrem
- **Solusi:** Imputasi median + SMOTE untuk oversampling kelas minoritas

## 📁 Struktur Direktori

```
MLOps-StrokePrediction/
├── .devcontainer/devcontainer.json  # Konfigurasi GitHub Codespaces
├── data/
│   ├── raw/          # Dataset asli dari Kaggle (tidak dimodifikasi)
│   ├── processed/    # Data setelah preprocessing
│   ├── interim/      # Batch simulasi bulanan (data01-05.csv)
│   └── external/     # Data referensi eksternal
├── models/
│   ├── trained/      # Model .pkl hasil training
│   └── evaluation/   # Metrics, confusion matrix
├── notebooks/
│   └── 01_initial_eda.ipynb  # EDA awal dataset stroke
├── src/
│   ├── data/         # ingestion.py, validate.py
│   ├── features/     # preprocess.py (imputasi, encoding, SMOTE)
│   ├── models/       # train.py, predict.py
│   └── visualization/ # eda_plots.py
├── config/config.yaml  # Hyperparameter & threshold konfigurasi
├── reports/figures/    # Grafik output EDA
├── tests/              # Unit tests
├── requirements.txt
└── README.md
```

## ⚡ Cara Menjalankan dengan GitHub Codespaces

1. Klik badge berikut untuk membuka lingkungan kerja secara instan:

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/anazahra/MLOps-StrokePrediction)

2. Tunggu setup otomatis selesai (~3-5 menit)
3. Semua dependencies otomatis terinstall dari `requirements.txt`
4. Verifikasi setup:
   ```bash
   python -c "import sklearn, mlflow, imblearn; print('Setup OK!')"
   ```
5. Upload dataset ke `data/raw/` dan buka `notebooks/01_initial_eda.ipynb`

## 🛠️ Setup Lokal (Alternatif)

```bash
git clone https://github.com/anazahra/MLOps-StrokePrediction.git
cd MLOps-StrokePrediction
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

## 🌳 Branching Strategy (GitHub Flow)

| Branch | Tujuan |
|--------|--------|
| `main` | Kode production-ready, hanya dari Pull Request |
| `feat/initial-eda` | EDA awal dataset stroke *(sudah di-merge)* |
| `feat/data-pipeline` | Pipeline ingestion & preprocessing |
| `feat/model-training` | Training Random Forest + MLflow |

## 👥 Mahasiswa 

**Ana Zahratul Firdausi** - 235150201111049
