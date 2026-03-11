# Surface Defect Finder – RTSP Vision Inspection System

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green)
![PyQt5](https://img.shields.io/badge/GUI-PyQt5-orange)
![RTSP](https://img.shields.io/badge/Streaming-RTSP-red)
![Industrial Vision](https://img.shields.io/badge/Application-Industrial%20Inspection-darkgreen)
![License](https://img.shields.io/badge/License-MIT-yellow)

An **industrial computer vision inspection system** designed to detect **surface defects on machined components** using reference image comparison and real-time camera feeds.

The system captures images from an **RTSP camera**, compares them against a **reference image**, and highlights deviations such as **scratches, dents, machining defects, or contamination**.

---

# Dashboard Preview

<p align="center">
<img width="1068" height="748" alt="image" src="surface_defect.png" />

</p>

---

# Key Features

### Industrial Vision Capabilities

* Real-time **RTSP camera inspection**
* **Reference image comparison**
* **Surface defect detection**
* **Automatic background removal**
* **High contrast defect highlighting**

### Annotation & Training

* Bounding box defect detection
* **YOLO label export**
* Fixed or **variable bounding box size**
* Dataset generation for **AI model training**

### User Interface

* Industrial **PyQt5 dashboard**
* Live camera preview
* Start / Stop inspection
* Defect count indicator
* Reference image selection

---

# System Architecture

```
                +---------------------+
                |     RTSP Camera     |
                +----------+----------+
                           |
                           v
                 +-------------------+
                 | Frame Acquisition |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 | Image Preprocess  |
                 | - Background remove
                 | - Normalization
                 +-------------------+
                           |
                           v
                 +-------------------+
                 | Reference Compare |
                 | (Difference Map)  |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 | Defect Detection  |
                 | - Contours        |
                 | - Thresholding    |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 | Annotation Engine |
                 | - Bounding boxes  |
                 | - YOLO labels     |
                 +-------------------+
                           |
                           v
                +----------------------+
                | PyQt5 Dashboard UI   |
                +----------------------+
```

---

# Workflow

1. Load or capture a **reference image**
2. Connect **RTSP camera**
3. Capture inspection frame
4. Perform **image preprocessing**
5. Compute **difference vs reference**
6. Detect **defect regions**
7. Draw bounding boxes
8. Export labels if needed

---

# Project Structure

```
surface-defect-finder
│
├── README.md
│
├── assets
│   ├── dashboard.png
│
├── src
│   ├── main.py
│   ├── gui.py
│   ├── defect_detection.py
│   ├── preprocessing.py
│   └── utils.py
│
├── reference
│   └── reference.png
│
├── outputs
│   ├── annotated_images
│   └── labels
│
└── requirements.txt
```

---

# Installation

## 1 Clone Repository

```bash
git clone https://github.com/yourusername/surface-defect-finder.git
cd surface-defect-finder
```

---

## 2 Create Virtual Environment

```bash
python -m venv .venv
```

Activate:

### Windows

```bash
.venv\Scripts\activate
```

### Linux / Mac

```bash
source .venv/bin/activate
```

---

## 3 Install Dependencies

```bash
pip install -r requirements.txt
```

Example requirements:

```
opencv-python
numpy
pyqt5
imutils
scikit-image
```

---

# Running the Application

```bash
python src/main.py
```

The dashboard will launch.

You can:

* Select **Reference Image**
* Enter **RTSP URL**
* Click **Start Inspection**

---

# RTSP Example

```
rtsp://admin:admin123@192.168.128.10:554/stream
```

---

# Example Output

Detected defects will appear as:

* **Bounding boxes**
* **Defect counter**
* **Annotated inspection image**

Example:

```
Defects Detected: 3
```

---

# Industrial Use Cases

### Automotive Manufacturing

Inspection of:

* Cylinder heads
* Brake components
* Cast parts
* Machined surfaces

### Precision Engineering

Detection of:

* Scratches
* Surface contamination
* Machining defects
* Missing features

### Production Line Integration

Can integrate with:

* PLC systems
* OPC UA
* Manufacturing dashboards
* Quality traceability systems

---

# Future Improvements

* Deep learning defect classification
* YOLO / Detectron integration
* Real-time **production line integration**
* Database logging (MongoDB / PostgreSQL)
* Industrial camera SDK support
* Edge deployment on **NVIDIA Jetson / Industrial PC**

---

# Author

**Karthikeyan**

Industrial Automation | Machine Vision | AI Inspection Systems

---

# License

MIT License

---

# Acknowledgements

* OpenCV community
* Industrial machine vision developers
* Python open-source ecosystem