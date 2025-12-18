<!-- # Initial file content.
git init
uv venv .venv
source .venv/bin/activate
uv pip install -r requirements.txt

dvc init
dvc add data/wine_sample.csv

dvc remote add -d wine-remote s3://<s3_bucket_name>
dvc push

git add data/wine_sample.csv.dvc

git remote add origin git@github.com:kioskOG/Wine-Prediction-Model.git
git add . && git commit -m "dvc with s3" && git push -u origin main -->

# 🍷 Wine Prediction Model

**ML dataset versioning with DVC + S3 backend**

This repository demonstrates how to version datasets using **DVC (Data Version Control)** with **Amazon S3** as a remote storage backend, while keeping code and metadata tracked via **Git**.

It’s designed as a **minimal, reproducible setup** that you can extend into a full ML pipeline later.

---

## 📦 Tech Stack

* **Python** (virtual environment managed with `uv`)
* **DVC** for dataset versioning
* **Amazon S3** as DVC remote storage
* **Git & GitHub** for source control

---

## 📂 Project Structure

```
Wine-Prediction-Model/
├── data/
│   └── wine_sample.csv        # Dataset (tracked by DVC)
├── data/wine_sample.csv.dvc   # DVC metadata file
├── .dvc/                      # DVC internal configs
├── .gitignore
├── requirements.txt
├── README.md
└── __init__.py
```

> ⚠️ **Important:**
> The actual dataset (`wine_sample.csv`) is **NOT stored in GitHub**.
> Only the `.dvc` file is committed. The data lives in **S3**.

---

## 🚀 Getting Started

### 1️⃣ Initialize Git repository

```bash
git init
```

---

### 2️⃣ Create & activate virtual environment

Using **uv** (recommended for speed and reproducibility):

```bash
uv venv .venv
source .venv/bin/activate
```

---

### 3️⃣ Install dependencies

```bash
uv pip install -r requirements.txt
```

---

## 📊 Dataset Versioning with DVC

### 4️⃣ Initialize DVC

```bash
dvc init
```

---

### 5️⃣ Add dataset to DVC tracking

```bash
dvc add data/wine_sample.csv
```

This will:

* Track the dataset via DVC
* Generate `data/wine_sample.csv.dvc`
* Automatically update `.gitignore` to exclude raw data

---

### 6️⃣ Configure S3 as DVC remote

```bash
dvc remote add -d wine-remote s3://<s3_bucket_name>
```

> Make sure your AWS credentials are configured:

```bash
aws configure
```

---

### 7️⃣ Push data to S3

```bash
dvc push
```

✅ Dataset is now safely stored in S3.

---

## 🧾 Git Version Control

### 8️⃣ Commit DVC metadata

```bash
git add data/wine_sample.csv.dvc .dvc/config .gitignore
git commit -m "Track dataset using DVC with S3 backend"
```

---

### 9️⃣ Add GitHub remote & push

```bash
git remote add origin git@github.com:kioskOG/Wine-Prediction-Model.git
git branch -M main
git push -u origin main
```

---

## 🔁 Reproducing the Dataset (For Other Users)

Anyone cloning this repo can restore the dataset by running:

```bash
git clone git@github.com:kioskOG/Wine-Prediction-Model.git
cd Wine-Prediction-Model

uv venv .venv
source .venv/bin/activate
uv pip install -r requirements.txt

dvc pull
```

📥 The dataset will be downloaded directly from **S3**.

---

## 🔐 Notes on Security & Best Practices

* Do **not** commit AWS credentials
* Use IAM roles or least-privilege IAM users
* Consider enabling:

  * S3 versioning
  * Server-side encryption (SSE-S3 / SSE-KMS)

---

## 🧠 Why DVC?

* Git-like workflows for data
* Reproducibility
* Cloud-agnostic storage
* Clean separation of **code vs data**

---
