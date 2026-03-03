# Demand Forecasting & Revenue Optimization Pipeline

## Project Overview

This project implements a dynamic pricing and revenue optimization system for a hotel property. The objective is to maximize revenue under demand uncertainty and inventory constraints by integrating forecasting, elasticity modeling, constrained optimization, and multi-period pricing simulation.

The system demonstrates how data-driven pricing decisions can significantly outperform static pricing strategies.

## Key Features

- **Time-Series Demand Forecasting**: Prophet-based forecasting with seasonality modeling and evaluation using MAE and RMSE
- **Price Elasticity Estimation**: Log-log regression framework to quantify demand response to price changes
- **Revenue Optimization**: Nonlinear optimization with business constraints (price bounds, inventory limits)
- **Capacity-Constrained Pricing**: Ensures demand does not exceed available inventory
- **Multi-Period Simulation**: 30-day booking horizon simulation comparing static vs optimized pricing
- **Revenue Impact Analysis**: Quantifies incremental revenue lift

## Dataset

The project uses the **Hotel Booking Demand Dataset (Kaggle)**.

Data includes:
- Arrival dates
- Average Daily Rate (ADR)
- Booking demand
- Cancellation indicators

Daily booking demand and average prices were aggregated to construct a pricing analytics dataset.

## Project Structure

```
dynamic-hotel-pricing-optimization/
│
├── data/
│   ├── raw/
│   │   └── hotel_bookings.csv
│   └── processed/
│       ├── daily_aggregated.csv
│       └── forecast_output.csv
│
├── notebooks/
│   ├── 01_data_preparation_and_eda.ipynb
│   ├── 02_demand_forecasting.ipynb
│   ├── 03_price_elasticity_modeling.ipynb
│   ├── 04_revenue_optimization.ipynb
│   └── 05_dynamic_pricing_simulation.ipynb
│
├── requirements.txt
└── README.md
```

## Methodology

### 1. Demand Forecasting

A Prophet time-series model was trained using historical daily booking demand.

**Performance Metrics:**

- MAE: 19.31
- RMSE: 23.74

The model captures trend and seasonality components to generate baseline demand estimates.

### 2. Price Elasticity Estimation

A log-log regression model was used:

log(Q) = β₀ + β₁ log(P)

Estimated Price Elasticity:

**0.408**

This indicates a positive relationship between price and demand at the aggregated level, suggesting structural demand effects or seasonality influencing observed pricing behavior.

### 3. Revenue Optimization

Revenue function:

R(P) = P × Q(P)

Two optimization scenarios were evaluated:

**Unconstrained Optimization**
- Optimal Price: 500.00
- Expected Revenue: 88,897.42

**Capacity-Constrained Optimization**
- Optimal Price: 190.96
- Expected Demand: 120 (capacity limit)
- Expected Revenue: 22,914.81

Business constraints applied:
- Price floor and ceiling
- Inventory limit (120 rooms)

### 4. Multi-Day Pricing Simulation

A 30-day booking horizon simulation compared:

- Static Pricing Strategy
- Revenue-Optimized Strategy

**Results:**

- Static Pricing Revenue: 11,839.60
- Optimized Pricing Revenue: 60,000.00
- Revenue Lift: 406.77%

This demonstrates the significant revenue impact of optimized pricing relative to naive static pricing.

## Technologies & Libraries

- Python
- pandas
- numpy
- Prophet
- scikit-learn
- SciPy
- matplotlib
- seaborn

## Outputs

The system generates:
- Demand forecasts with uncertainty
- Estimated price elasticity coefficient
- Revenue-maximizing price recommendations
- Capacity-aware pricing strategy
- Multi-period revenue simulation
- Revenue lift quantification

## Business Impact

This project demonstrates the ability to:

- Build forecasting models at appropriate aggregation levels
- Quantify price sensitivity using econometric modeling
- Construct constrained nonlinear optimization models
- Generate actionable price recommendations
- Measure incremental revenue impact

The approach mirrors real-world revenue management workflows used in hospitality and admissions pricing environments.
