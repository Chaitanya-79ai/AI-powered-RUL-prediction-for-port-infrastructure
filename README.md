# 🚢 AI-Powered RUL Prediction for Port Infrastructure
> Predicting Remaining Useful Life (RUL) using CMAPSS sensor data, LSTM networks, and a FastAPI-powered inference system.
>
> ## 📘 Overview

Modern ports rely heavily on complex machinery like cranes, RTGs, and other heavy equipment that must operate with minimal downtime. Unexpected breakdowns not only delay operations but also incur significant maintenance costs. This project presents an AI-powered predictive maintenance system that forecasts equipment failure in advance by predicting the Remaining Useful Life (RUL) of machines using sensor data.

Leveraging the NASA CMAPSS FD001 dataset — a widely used benchmark for time-series degradation modeling — this system processes multivariate sensor data, learns degradation patterns through Long Short-Term Memory (LSTM) networks, and serves real-time RUL predictions through a FastAPI-based REST API. The entire pipeline is experiment-tracked via MLflow and containerized using Docker for easy deployment in cloud or edge environments.

This project showcases how machine learning and modern MLOps tools can be integrated into a robust solution to reduce maintenance costs, improve asset longevity, and ensure smoother operations in high-throughput port environments.

