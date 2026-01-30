# 🌾 AI-Powered Crop Recommendation System
## Intelligent Decision Support for Indian Farmers 🇮🇳

[![Databricks](https://img.shields.io/badge/Databricks-Unified%20Analytics-red?logo=databricks&style=for-the-badge)](https://databricks.com/)
[![MLflow](https://img.shields.io/badge/MLflow-Model%20Registry-blue?logo=mlflow&style=for-the-badge)](https://mlflow.org/)
[![Delta Lake](https://img.shields.io/badge/Delta%20Lake-ACID%20Transactions-green?logo=deltalake&style=for-the-badge)](https://delta.io/)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&style=for-the-badge)](https://www.python.org/)

---

## 🎯 Executive Summary
This project solves the "What should I grow?" dilemma for Indian farmers by combining **Agronomic Science** (soil/climate viability) with **Economic Forecasting** (market price trends). 

Unlike traditional systems that only check if a crop *can* grow, our dual-AI approach ensures farmers choose crops that are both **biologically viable** and **economically profitable**.

---

## 📋 Problem Statement

### The Challenge
Indian farmers face critical decisions each planting season. Making the wrong choice leads to:
- 📉 **Yield Loss**: Up to 30% loss due to unsuitable soil/climate conditions.
- 💰 **Financial Ruin**: Market price crashes can wipe out a season's earnings.
- 🌍 **Soil Degradation**: Improper crop rotation damages long-term soil health.

### Why Traditional Methods Fail
1. **Complexity**: Crop suitability depends on 7+ interconnected environmental factors.
2. **Market Volatility**: Prices fluctuate wildly; a good harvest means nothing if prices crash.
3. **Data Silos**: Farmers cannot manually analyze 20 years of soil, weather, and market data.

### 💡 Our Solution: Dual-Model AI Strategy

1. **🧑‍🌾 The Agronomist (Random Forest)**: *"Can this crop grow here?"*
   - Analyzes N, P, K, pH, Temperature, Humidity, and Rainfall.
   - **88% Accuracy** in predicting crop viability.

2. **💼 The Economist (Facebook Prophet)**: *"Should I grow this crop?"*
   - Forecasts market prices 12 months into the future.
   - Calculates **Risk Volatility** and **Projected ROI**.

---

## 🏗️ Technical Architecture

We utilize the **Databricks Medallion Architecture** to transform raw data into actionable insights.

```mermaid
graph TD
    subgraph Bronze [Bronze Layer - Raw Data]
        B1[(Kaggle Crop Data)]
        B2[(State Weather)]
        B3[(Mandi Prices)]
        B4[(Soil Profiles)]
    end

    subgraph Silver [Silver Layer - Cleaned & Enriched]
        S1[Normalized Crop Names]
        S2[Imputed Missing Values]
        S3[Feature Engineering]
        S4[State Aggregations]
    end

    subgraph Gold [Gold Layer - ML & Business Aggregates]
        G1{{Agronomist Model<br/>Random Forest}}
        G2{{Economist Model<br/>Prophet Time-Series}}
        G3[ROI & Risk Calculator]
    end

    subgraph UI [User Interface]
        User((Farmer))
        Dashboard[Databricks Notebook UI]
    end

    B1 --> S1
    B2 --> S4
    B3 --> S1
    B4 --> S2
    
    S1 --> S3
    S2 --> S3
    S4 --> S3
    
    S3 --> G1
    S3 --> G2
    
    G1 --> G3
    G2 --> G3
    G3 --> Dashboard
    User --> Dashboard
