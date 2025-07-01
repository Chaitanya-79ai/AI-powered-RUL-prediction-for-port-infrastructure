# 🚢 AI-Powered RUL Prediction for Port Infrastructure
> Predicting Remaining Useful Life (RUL) using CMAPSS sensor data, LSTM networks, and a FastAPI-powered inference system.


## 📘 Abstract

Port equipment like cranes and heavy machinery undergo gradual wear and can fail unexpectedly if not monitored properly. This project builds a predictive maintenance system that estimates the Remaining Useful Life (RUL) of such machinery using time-series sensor data.

We use the NASA CMAPSS FD001 dataset, which simulates sensor readings from aircraft engines operating under a single consistent condition and fault mode. The system learns degradation trends using both traditional machine learning (Random Forest) and deep learning models (LSTM). The model outputs RUL estimates based on historical sensor behavior.

The workflow includes preprocessing the time-series data, training models, tracking experiments using MLflow, and exposing the final model via a FastAPI-based REST API. The entire solution is containerized using Docker, making it ready for cloud or local deployment.

This project is a proof of concept for how predictive maintenance can be implemented using real-world-like sensor data, with a focus on reliable model tracking, clean API deployment, and modular design — potentially applicable to port equipment where similar degradation patterns occur.


## 📊 Dataset

This project uses the **CMAPSS (Commercial Modular Aero-Propulsion System Simulation)** dataset provided by NASA, which simulates sensor measurements from a fleet of aircraft engines over time. Although originally designed for aviation, it is widely used as a benchmark for developing and evaluating predictive maintenance algorithms — making it suitable for port machinery simulations.

We specifically use the **FD001 subset**, which includes:

- ✅ 100 training engine trajectories (each from start until failure)
- ✅ 100 test engine trajectories (each ending before failure)
- ✅ A separate file containing the true Remaining Useful Life (RUL) values for each engine in the test set

Each row in the dataset represents one operational cycle of a particular engine and includes:

| Column # | Description                |
|----------|----------------------------|
| 1        | Engine ID (unit number)    |
| 2        | Time in operational cycles |
| 3–5      | Operational settings (3 total) |
| 6–26     | Sensor measurements (21 sensors) |

- All engines start in a healthy condition and degrade over time.
- Only **one fault mode** (HPC degradation) and **one operating condition** are present in FD001 — making it ideal for a baseline model.

### 📁 Files Used

- `train_FD001.txt` — Full run-to-failure data for each engine (used for training)
- `test_FD001.txt` — Partial trajectories (we predict remaining cycles)
- `RUL_FD001.txt` — Ground truth RUL values for the test set

### 📎 Source

NASA Prognostics Center of Excellence:  
[https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data](https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data)

---




