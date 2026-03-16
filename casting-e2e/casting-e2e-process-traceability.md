# Pressure Die casting Traceability & Process Violation Monitoring

### Die Casting Shot Traceability • Process Limits • Quality Validation

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![IIoT](https://img.shields.io/badge/Industry-IIoT-green)
![MongoDB](https://img.shields.io/badge/Database-MongoDB-darkgreen)
![Analytics](https://img.shields.io/badge/Analytics-Process%20Monitoring-orange)
![Dashboard](https://img.shields.io/badge/UI-Industrial%20Dashboard-purple)
![License](https://img.shields.io/badge/License-MIT-yellow)

An **industrial traceability and process validation dashboard** designed for **Buhler aluminum die casting machines**.

The system monitors **shot-level production data**, validates **process parameters against control limits**, and highlights **process violations that lead to casting defects**.

It provides engineers with **real-time visibility into process stability and traceability compliance**.

---

# Dashboard Preview

<p align="center">
<img src= casting-e2e-process.png>
          </p>

The dashboard visualizes:

* Real-time shot traceability
* Biscuit thickness trends
* Process limit violations
* Quality distribution
* Production shot history

---

# System Purpose

Die casting quality is highly dependent on **stable process parameters**.

This system ensures:

✔ Full **shot-to-part traceability**
✔ **Process parameter monitoring**
✔ **Violation detection against limits**
✔ **Early defect detection**

---

# Industrial Architecture

```
Buhler Die Casting Machine
          │
          │ Process Sensors
          ▼
Machine Controller / PLC
          │
          ▼
Production Data Logger
          │
          ▼
MongoDB Database
          │
          ▼
Traceability Validation Engine
          │
          ▼
Process Limit Analyzer
          │
          ▼
Industrial Monitoring Dashboard
```

---

# Process Parameter Monitoring

The system monitors key die casting parameters including:

| Parameter              | Description                |
| ---------------------- | -------------------------- |
| Biscuit Thickness      | Remaining metal after shot |
| Metal Pressure         | Maximum metal press        |
| Injection Time         | Injection duration         |
| Cycle Time             | Shot cycle duration        |
| Plunger Speed          | Injection plunger velocity |
| Metal at Gate          | Metal flow to gate         |
| Intensification Stroke | Pressure stroke            |

These parameters are validated for **each shot**.

---

# Process Limits (Control Limits)

Example monitored parameter:

### Biscuit Thickness

```
LSL = 25
USL = 35
```

Visualization logic:

| Indicator   | Meaning           |
| ----------- | ----------------- |
| Green Trend | Normal process    |
| Yellow Dot  | LOT / LOK warning |
| Red Dot     | Process violation |

Only **violations and warnings** are highlighted to simplify monitoring.

---

# Process Violation Detection

The system identifies violations when process parameters exceed defined limits.

Example violation rule:

```
if biscuit_thickness < LSL or biscuit_thickness > USL:
    quality = "BAD"
```

Warnings are triggered when parameters approach limits.

```
LOT / LOK
```

---

# Quality Classification Logic

| Status | Meaning                         |
| ------ | ------------------------------- |
| OK     | Process within limits           |
| LOT    | Near upper/lower limit          |
| LOK    | Slight deviation but acceptable |
| BAD    | Process violation               |

Example quality summary:

```
Total Shots: 168
OK: 150
BAD: 10
LOT/LOK: Remaining
```

---

# Traceability Data Model

Each record represents **one die casting shot**.

Example record:

```json
{
  "shot_timestamp": "2026-02-28 06:54:27",
  "production_counter": 1060340,
  "die_shot_counter": 389,
  "machine_status": "ON",
  "marking_code": "ODB1898",
  "marking_timestamp": "2026-02-28 06:55:27",
  "quality": "ok",
  "biscuit_thickness": 34,
  "cycle_time": 8.152,
  "injection_time": 6.04
}
```

---

# Dashboard Components

## Production KPIs

Displays latest machine state:

* Latest marking code
* Latest shot ID
* Marking timestamp
* File timestamp
* Quality distribution

---

# Biscuit Thickness Trend

Displays **latest 300 shots**.

Features:

✔ Process trend line
✔ LSL / USL limits
✔ Violation highlighting
✔ Warning indicators

---

# Shot Traceability Table

The dashboard shows detailed production history.

Fields include:

| Field                  | Description             |
| ---------------------- | ----------------------- |
| Shot Timestamp         | Machine shot time       |
| Production Counter     | Total production count  |
| Die Shot Counter       | Die-specific shot count |
| Machine Status         | ON / OFF                |
| Marking Code           | Part traceability code  |
| Marking Timestamp      | Marking machine time    |
| Shot Interval          | Time between shots      |
| Quality                | OK / LOT / BAD          |
| Part Code              | Produced component      |
| Intensification Stroke | Casting stroke          |
| Max Metal Pressure     | Metal pressure          |
| Biscuit Thickness      | Remaining metal         |
| Metal at Gate          | Metal flow              |
| Cycle Time             | Shot cycle              |
| Injection Time         | Injection duration      |
| Plunger Speed          | Injection velocity      |

---

# Dashboard Filters

Users can filter the dashboard using:

| Filter    | Description      |
| --------- | ---------------- |
| Mode      | LIVE / HIST      |
| Date      | Production date  |
| Shift     | Shift A / B / C  |
| Quality   | OK / BAD / ALL   |
| Page Size | Records per page |

---

# Process Violation Use Case

Example scenario:

```
Shot 382
Biscuit thickness = 54
USL = 35
```

System classification:

```
QUALITY = BAD
PROCESS VIOLATION
```

The dashboard highlights this shot in **red** for quick identification.

---

# Installation

Clone repository:

```bash
git clone https://github.com/yourusername/buhler-traceability-validation.git
cd buhler-traceability-validation
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# Running the Dashboard

Start server:

```bash
python app.py
```

Open dashboard:

```
http://localhost:5000/dashboard
```

---

# Industrial Benefits

This system helps manufacturing plants:

✔ Maintain **process stability**
✔ Ensure **full traceability**
✔ Detect **casting defects early**
✔ Reduce **scrap rate**
✔ Support **quality audits**

---

# Future Improvements

Planned upgrades:

* AI-based defect prediction
* SPC control charts
* OEE monitoring
* Multi-machine monitoring (1800 / 4400)
* Predictive maintenance alerts

---

# Author

Karthikeyan
Industrial Automation • IIoT • Smart Foundry Systems

---

# License

MIT License
