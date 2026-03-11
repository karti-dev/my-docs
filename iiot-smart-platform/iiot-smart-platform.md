# IIoT Multi-Defect Predictor

### Aluminum Die Casting - AI + Golden Limits + Smart Dashboard

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![IIoT](https://img.shields.io/badge/Industry-IIoT-green)
![Machine Learning](https://img.shields.io/badge/AI-Multi--Defect%20Prediction-orange)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-darkgreen)
![API](https://img.shields.io/badge/API-FastAPI-red)
![License](https://img.shields.io/badge/License-MIT-yellow)

<p align="center">
<img src= iiot-smart-platform.png>
          </p>
Industrial **AI-driven defect prediction system** for **Aluminum Die Casting machines** using **process sensor data, golden limits, and machine learning**.

The platform predicts casting defects such as:

* Porosity
* Blow Hole
* Cold Shut
* Shrinkage
* Misrun

using **shot parameters collected from IIoT systems**.

The system includes:

* **Golden limit generation**
* **Multi-defect ML prediction**
* **Rule-based fallback detection**
* **MongoDB shot data integration**
* **Real-time dashboard**

---

# System Overview

The project performs three core functions:

1. **Golden Limits Generator**

Builds baseline parameter ranges from **OK / GOOD shots**.

2. **Text Log Parser**

Converts **machine shot logs** into structured data.

3. **Multi-Defect Prediction**

Predicts casting defects using **machine learning models**.

---

# Industrial Architecture

```text
        Die Casting Machine (T)
                 │
                 │ Shot Data
                 ▼
           IIoT Data Logger
                 │
                 ▼
              MongoDB
             Database: iiot
             Collection: 
                 │
                 ▼
         Golden Limits Engine
                 │
                 ▼
        Multi-Defect ML Model
                 │
         ┌───────┴────────┐
         ▼                ▼
   Rule-Based Engine    Prediction API
         │                │
         ▼                ▼
     Alerts & KPIs   Smart Dashboard
```

---

# Database Configuration

MongoDB Database

```text
Database: iiot
Collection: 
```

Each document represents a **machine shot record** with process parameters.

---

# Supported Process Parameters

The system reads the following machine parameters directly from the dataset:

```
p_N_Mul
ΣCyc_tot
p_IM_R0
s_Tr_v>p
s_MA
s_Pre
p_IMmax
p_M
sumCycJob
l_B
F_L
p_N_Acc
t_Cyc
tC_Lub
v_MA
v_CF
t_F
t_I
s_Ffin
t_Σ
Tr_v>p
Σ_PRDtot
```

Unicode column names are fully supported.

---

# Project Structure

```
iiot-multidefect-predictor
│
├── main_api.py
│
├── app
│   ├── rules
│   │   └── defect_rules.py
│
├── models
│   ├── datasets
│   │   ├── _ok.csv
│   │   ├── _defects_train.csv
│   │
│   ├── golden_limits_.json
│   ├── multi_defect_model.pkl
│   ├── feature_columns_.json
│   └── defect_classes.json
│
├── tools
│   ├── generate_golden_limits.py
│   ├── parse_shot_text.py
│   └── train_multidefect_model.py
│
├── .env
└── requirements.txt
```

---

# Installation

Clone the repository

```bash
git clone https://github.com/yourusername/iiot-multidefect-predictor.git
cd iiot-multidefect-predictor
```

Install dependencies

```bash
pip install -r requirements.txt
```

Create environment file

```bash
cp .env.example .env
```

---

# Dataset Configuration

## A) OK / GOOD Shots (Golden Limits)

Place baseline dataset:

```
models/datasets/_ok.csv
```

or

```
models/datasets/_good_shot.json
```

Update `.env`

```
GOOD_SHOTS_PATH=models/datasets/_ok.csv
```

---

## B) Labeled Defect Dataset

Provide a dataset containing defect labels.

Supported formats:

```
models/datasets/_defects_train.csv
models/datasets/_defects_train.json
```

Example labels:

```
porosity
blow_hole
cold_shut
shrinkage
misrun
```

CSV labels should contain binary columns:

```
porosity,blow_hole,cold_shut
0,1,0
```

Update `.env`

```
TRAIN_DATA_PATH=models/datasets/_defects_train.csv
```

---

# Generate Golden Limits

Golden limits define **normal operating ranges**.

Run:

```bash
python tools/generate_golden_limits.py
```

Output:

```
models/golden_limits_.json
```

---

# Parse Machine Shot Logs

Convert raw machine logs into JSON format.

Example input:

```
p N Mul * = 1967 ; Nitrogen pressure
```

Run parser:

```bash
python tools/parse_shot_text.py --infile sample_shot.txt --outfile out.json
```

Output:

```
out.json
```

---

# Train Multi-Defect Model

Train the machine learning model.

```bash
python tools/train_multidefect_model.py
```

Generated models:

```
models/multi_defect_model.pkl
models/feature_columns_.json
models/defect_classes.json
```

---

# Start Prediction API

Run the prediction service.

```bash
python main_api.py
```

Server runs at:

```
http://localhost:8000
```

---

# API Endpoints

Health Check

```
GET /health
```

Golden Limits

```
GET /golden/limits
```

Check Limit Violations

```
POST /golden/check
```

Predict Defects from Latest Shot

```
GET /predict/latest
```

Predict Using Object ID

```
POST /predict
```

Example:

```bash
curl -X POST http://localhost:8000/predict \
-H "Content-Type: application/json" \
-d '{"object_id":"691308ce98c48369c48cee5e"}'
```

---

# Rule-Based Prediction (Fallback)

If the ML model is not available, the system automatically switches to **rule-based prediction**.

Rules are located in:

```
app/rules/defect_rules.py
```

Check active rules:

```
GET /rules
```

---

# Smart Dashboard

Start API:

```bash
python main_api.py
```

Open dashboard:

```
http://localhost:8000/dashboard
```

Dashboard features:

* Shot timeline
* KPI metrics
* Process trend visualization
* Defect alerts
* Rule explanations

---

# Dashboard Widgets

Version 7 Dashboard includes:

### Shot Drill-Down

Click a shot to see:

* parameter violations
* defect explanation

### Violation Heatmap

Displays most violated parameters vs hour.

### Defect Distribution

Donut chart showing defect proportions.

---

# Model Training Tips

To improve model accuracy:

* Collect **500+ samples per defect**
* Handle dataset imbalance
* Use **golden limit deviation features**

Important engineered features:

```
hard_count
max_abs_z
out_ratio
```

Also include context features if available:

```
machineId
castingIdent
recipe
shift
```

---

# 4400 Machine Setup

Add baseline dataset:

```
models/datasets/4400_ok.csv
```

Generate limits:

```bash
python -m tools.generate_golden_limits
```

Start system:

```bash
python main_api.py
```

Open dashboard:

```
http://localhost:8000/dashboard
```

---

# Industrial Applications

This system can be used for:

* Aluminum die casting quality prediction
* Early defect detection
* Process parameter monitoring
* Smart foundry analytics
* Predictive manufacturing

---

# Author

Karthikeyan
Industrial Automation | IIoT | AI for Manufacturing

---

# License

MIT License

