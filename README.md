# 🚢 Predictive Maintenance: Ship Engine Anomaly Detection System

> **An ensemble outlier detection engine that flags critical engine failures with <1% false positive rate.**

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![ML](https://img.shields.io/badge/Model-Isolation_Forest_|_SVM-green.svg)
![Status](https://img.shields.io/badge/Status-Prototype-yellow.svg)

## 🚨 The Business Problem
Unexpected ship engine failures lead to massive delivery delays, safety hazards, and fuel inefficiency. However, traditional monitoring systems often trigger too many false alarms, causing "alert fatigue" for engineering teams.

**Goal:** Build a high-precision anomaly detection system that filters out noise and only flags "High Confidence" critical failures for immediate inspection.

## 🛠️ The Solution (Ensemble Engine)
Instead of relying on a single algorithm, this project implements a **Multi-Vote Consensus System**. An engine reading is only flagged if it triggers all three independent detection layers:

1.  **Statistical Layer (IQR):** Flags extreme deviations in **2+ simultaneous sensors** (e.g., Oil Pressure + Coolant Temp).
2.  **Geometric Layer (One-Class SVM):** Captures complex, non-linear boundaries of "normal" operation (tuned with RBF kernel).
3.  **Isolation Layer (Isolation Forest):** Efficiently isolates anomalies by identifying data points with short decision paths.

## 📊 Key Results & Impact
*   **Noise Reduction:** The baseline IQR method flagged **24%** of data as anomalous—operationally useless.
*   **Precision Engineering:** By enforcing the **Ensemble Intersection Rule** (Intersection of Method 1, 2, & 3), the system reduced alerts to **190 critical events (<1% of data)**.
*   **Operational Value:** This provides a manageable "High Priority" ticket queue that engineers can realistically investigate without ignoring the system.

## 💻 Tech Stack
*   **Core:** Python, Pandas, NumPy
*   **Modelling:** Scikit-Learn (IsolationForest, OneClassSVM)
*   **Visualization:** Matplotlib, Seaborn, PCA (Principal Component Analysis for 2D projection)

## 📉 Visualizing the Anomalies
*   **Box Plot Analysis:** Initial EDA revealed significant outliers in *Fuel Pressure* and *RPM*, validating the need for robust scaling.
*   **PCA Projection:** Dimensionality reduction to 2D proved that anomalies (Red) lie on the fringes of the cluster, though the complex 6D structure requires non-linear models (SVM) to fully separate.
