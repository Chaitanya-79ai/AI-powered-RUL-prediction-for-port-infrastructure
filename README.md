# 🚢 AI-Powered RUL Prediction for Port Infrastructure
> Predicting Remaining Useful Life (RUL) using CMAPSS sensor data, LSTM networks, and a FastAPI-powered inference system.
>
> ## 📘 Abstract

Port equipment like cranes and heavy machinery undergo gradual wear and can fail unexpectedly if not monitored properly. This project builds a predictive maintenance system that estimates the Remaining Useful Life (RUL) of such machinery using time-series sensor data.

We use the NASA CMAPSS FD001 dataset, which simulates sensor readings from aircraft engines operating under a single consistent condition and fault mode. The system learns degradation trends using both traditional machine learning (Random Forest) and deep learning models (LSTM). The model outputs RUL estimates based on historical sensor behavior.

The workflow includes preprocessing the time-series data, training models, tracking experiments using MLflow, and exposing the final model via a FastAPI-based REST API. The entire solution is containerized using Docker, making it ready for cloud or local deployment.

This project is a proof of concept for how predictive maintenance can be implemented using real-world-like sensor data, with a focus on reliable model tracking, clean API deployment, and modular design — potentially applicable to port equipment where similar degradation patterns occur.


