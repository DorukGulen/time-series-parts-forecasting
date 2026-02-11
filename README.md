# 📈 Federated Time Series Forecasting

A privacy-preserving federated learning system for time series sales
forecasting using Flower (flwr).\
This project trains a global forecasting model collaboratively across
decentralized edge devices without sharing raw data.

------------------------------------------------------------------------

## 🚀 Project Overview

This project implements a **Federated Learning (FL)** framework for
monthly sales forecasting.

Instead of centralizing data, multiple clients: - Train models locally
on private datasets - Share only model parameters with the central
server - Contribute to a global model using the **FedAvg** aggregation
strategy

The system compares **IID vs Non-IID data distributions** to analyze
convergence behavior and performance differences in federated
environments.

------------------------------------------------------------------------

## 🏗 System Architecture

-   **Central Server (PC/Laptop)**
    -   Aggregates model weights
    -   Coordinates federated rounds
    -   Uses Flower (flwr)
-   **Edge Clients (Raspberry Pi 5)**
    -   Train locally on partitioned datasets
    -   Use MLP or LSTM models
    -   Send weight updates only
-   **Communication**
    -   gRPC-based Flower protocol
    -   Same local network

Federated Loop:

Global Model → Local Training → Weight Updates → Aggregation → New
Global Model

------------------------------------------------------------------------

## 📊 Dataset

-   Dataset: Superstore Sales Dataset (Kaggle)
-   \~10,000 rows
-   Transaction-level retail data
-   Aggregated into **monthly total sales**

### Time Series Construction

-   Lookback window: 12 months
-   Forecast horizon: 1 month
-   Monthly aggregation (sum)
-   Sliding window supervised learning setup

------------------------------------------------------------------------

## 🔀 Data Partitioning

### 1️⃣ IID Split

-   Random shuffle
-   Equal 50/50 division
-   Balanced statistical distribution

### 2️⃣ Non-IID Split (Value-Based)

-   Threshold-based split on sales
-   Client 0 → Sales ≤ threshold
-   Client 1 → Sales \> threshold

------------------------------------------------------------------------

## 🧠 Models

### 🔹 MLP (Baseline)

-   Fully connected network
-   Flattened input windows

### 🔹 LSTM (Sequence-aware)

-   Preserves temporal structure
-   Captures sequential dependencies

------------------------------------------------------------------------

## 📏 Evaluation Metrics

-   MSE (Mean Squared Error)
-   MAE (Mean Absolute Error)
-   MAPE
-   SMAPE
-   R² Score

------------------------------------------------------------------------

## 📉 Results Summary

### IID Scenario

-   Faster convergence
-   Smoother training
-   Lower error metrics

### Non-IID Scenario

-   Slower convergence
-   More realistic federated learning setup

> Federated learning is feasible in both settings, but IID distributions
> converge faster.

------------------------------------------------------------------------

## 🖥 Deployment

``` bash
# Start server
python server.py

# Start client
python client.py --server-ip <SERVER_IP>
```

------------------------------------------------------------------------

## 📂 Project Structure

    .
    ├── server.py
    ├── client.py
    ├── dataset.py
    ├── partition.py
    ├── models.py
    ├── train.py
    ├── requirements.txt
    └── plots/

------------------------------------------------------------------------

## 🔬 Key Contributions

-   Federated learning implementation using Flower
-   IID vs Non-IID comparison
-   Time-series forecasting pipeline
-   Edge-device deployment

------------------------------------------------------------------------

## 🛠 Tech Stack

-   Python
-   PyTorch
-   Flower (flwr)
-   Pandas
-   NumPy
-   Raspberry Pi 5

------------------------------------------------------------------------

## 📌 Future Improvements

-   FedProx integration
-   More clients
-   Transformer-based forecasting

