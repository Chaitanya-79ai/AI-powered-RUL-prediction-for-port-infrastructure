#  AI-Powered RUL Prediction for Port Infrastructure
> Predicting Remaining Useful Life (RUL) using CMAPSS sensor data, LSTM networks, and a FastAPI-powered inference system.

---

##  Abstract

Port equipment like cranes and heavy machinery undergo gradual wear and can fail unexpectedly if not monitored properly. This project builds a predictive maintenance system that estimates the Remaining Useful Life (RUL) of such machinery using time-series sensor data.

We use the NASA CMAPSS FD001 dataset, which simulates sensor readings from aircraft engines operating under a single consistent condition and fault mode. The system learns degradation trends using both traditional machine learning (Random Forest) and deep learning models (LSTM). The model outputs RUL estimates based on historical sensor behavior.

The workflow includes preprocessing the time-series data, training models, tracking experiments using MLflow, and exposing the final model via a FastAPI-based REST API. The entire solution is containerized using Docker, making it ready for cloud or local deployment.

---

##  Dataset

This project uses the **CMAPSS (Commercial Modular Aero-Propulsion System Simulation)** dataset provided by NASA, which simulates sensor measurements from a fleet of aircraft engines over time. Although originally designed for aviation, it is widely used as a benchmark for developing and evaluating predictive maintenance algorithms — making it suitable for port machinery simulations.

We specifically use the **FD001 subset**, which includes:

-  100 training engine trajectories (each from start until failure)
-  100 test engine trajectories (each ending before failure)
-  A separate file containing the true Remaining Useful Life (RUL) values for each engine in the test set

Each row in the dataset represents one operational cycle of a particular engine and includes:

| Column # | Description                |
|----------|----------------------------|
| 1        | Engine ID (unit number)    |
| 2        | Time in operational cycles |
| 3–5      | Operational settings (3 total) |
| 6–26     | Sensor measurements (21 sensors) |

- All engines start in a healthy condition and degrade over time.
- Only **one fault mode** (HPC degradation) and **one operating condition** are present in FD001 — making it ideal for a baseline model.

###  Files Used

- `train_FD001.txt` — Full run-to-failure data for each engine (used for training)
- `test_FD001.txt` — Partial trajectories (we predict remaining cycles)
- `RUL_FD001.txt` — Ground truth RUL values for the test set

### 📎 Source

NASA Prognostics Center of Excellence:  
[https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data](https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data)

---

##  Problem Statement

The objective of this project is to develop a system that predicts the **Remaining Useful Life (RUL)** of industrial machinery based on historical sensor data. Accurate RUL estimation enables predictive maintenance — helping minimize unplanned downtime and reduce maintenance costs.

We simulate this scenario using the **FD001 subset** from the NASA CMAPSS dataset, which provides multivariate time-series sensor data for engines operating under a single condition and degrading due to a single fault type. The task is to estimate, for each engine, how many cycles remain before failure based on its sensor behavior up to a given point.

This is framed as a **regression problem**, where the model predicts the number of remaining cycles. Two approaches are explored:
- A baseline using **Random Forest** for tabular RUL prediction
- A deep learning model using **LSTM** for capturing temporal degradation patterns

---

##  Tech Stack

This project uses the following technologies and tools:

###  Programming & Libraries
- **Python** – Core programming language
- **NumPy & pandas** – Data manipulation and feature engineering
- **scikit-learn** – Traditional machine learning (Random Forest)
- **TensorFlow / Keras** – Deep learning (LSTM model)
- **Matplotlib & Seaborn** – Visualization

###  Model Management & Tracking
- **MLflow** – Experiment tracking, model versioning, and logging

###  API Development
- **FastAPI** – Building and testing REST endpoints for model inference

###  Packaging & Deployment
- **Docker** – Containerization of the API for deployment

---

##  System Architecture / Pipeline

The end-to-end predictive maintenance pipeline consists of the following stages:

1. **Data Ingestion**  
   Load and parse the FD001 dataset (train/test/RUL) into structured DataFrames.

2. **Data Preprocessing & Feature Engineering**  
   - Normalize sensor values  
   - Create derived features (e.g., cycle count, moving averages, lags)  
   - Align training and test sets with RUL targets

3. **Model Training**  
   - Train a baseline **Random Forest** regression model  
   - Train an **LSTM** model to capture temporal degradation patterns

4. **Experiment Tracking**  
   - Use **MLflow** to log hyperparameters, model metrics, and artifacts

5. **Model Inference API**  
   - Build a REST API using **FastAPI**  
   - Accept input JSON and return predicted RUL for a given machine snapshot

6. **Containerization**  
   - Package the entire API with **Docker**  

---

###  Pipeline Diagram

```mermaid
graph TD
    A[Raw CMAPSS FD001 Data] --> B[Data Preprocessing]
    B --> C[Feature Engineering]
    C --> D1[Random Forest Model]
    C --> D2[LSTM Model]
    D1 & D2 --> E[MLflow Tracking]
    D2 --> F[FastAPI Inference Server]
    F --> G[Docker Container]


---







