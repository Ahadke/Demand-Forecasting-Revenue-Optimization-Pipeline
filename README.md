# Demand Forecasting & Revenue Optimization Pipeline

## Project Overview

This project implements an end-to-end dynamic pricing and revenue optimization system for a capacity-constrained hospitality environment. The objective is to maximize revenue under demand uncertainty by integrating SQL-based data engineering, de-trended price elasticity modeling, constrained nonlinear optimization, and multi-period dynamic programming.

The system mirrors real-world revenue management workflows used in admissions pricing and hospitality analytics.

---

## Key Features

- **SQL-Based Demand Aggregation** – Warehouse-style aggregation simulating Snowflake workflows
- **Time-Series Demand Forecasting** – Prophet-based forecasting with MAE and RMSE evaluation
- **De-trended Price Elasticity Estimation** – Residual-based log-log regression to mitigate price endogeneity
- **Constrained Revenue Optimization** – Nonlinear optimization with price bounds and capacity limits
- **Dynamic Programming Pricing** – Multi-period inventory-aware pricing via Bellman recursion
- **A/B Pricing Experimentation** – Statistical testing of static vs optimized pricing strategies
- **Revenue Lift Quantification** – Measured incremental revenue impact

---

## Dataset

This project uses the **Hotel Booking Demand Dataset (Kaggle)**.

Booking-level transactional data was aggregated into daily demand tables using SQL group-by operations before modeling.

Data includes:
- Arrival dates
- Average Daily Rate (ADR)
- Booking demand
- Cancellation indicators

---

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
│   ├── 00_sql_data_preparation_example.ipynb
│   ├── 01_data_preparation_and_eda.ipynb
│   ├── 02_demand_forecasting.ipynb
│   ├── 03_price_elasticity_modeling.ipynb
│   ├── 04_revenue_optimization.ipynb
│   ├── 05_dynamic_pricing_simulation.ipynb
│   └── 06_dynamic_programming_pricing.ipynb
│
├── requirements.txt
└── README.md
```

---

## Methodology

### 1. Demand Forecasting

A Prophet time-series model was trained on daily aggregated demand.

**Performance Metrics:**
- MAE: 19.31  
- RMSE: 23.74  

The model captures trend and seasonal components to estimate baseline demand independent of pricing effects.

---

### 2. Price Elasticity Estimation

To mitigate price endogeneity, demand was first de-trended using Prophet residuals.

Log-log regression:

log(residual_demand) ~ log(price)

Estimated Elasticity:
**−0.02**

This indicates demand is weakly price-sensitive after controlling for seasonality, suggesting structural demand drivers dominate short-term price response.

---

### 3. Revenue Optimization

Revenue function:

R(P) = P × Q(P)

Applied:
- Price floor and ceiling
- Capacity constraint (120 units)
- Nonlinear constrained optimization (SciPy)

Generated actionable price recommendations under operational limits.

---

### 4. Dynamic Programming

Implemented multi-period optimization:

Vₜ(s) = maxₚ [ P × Q(P) + Vₜ₊₁(s − Q(P)) ]

Where:
- s = remaining inventory
- t = time period

Produced optimal price path across a 30-day booking horizon.

---

### 5. A/B Pricing Simulation

Simulated:

- Control: static pricing
- Treatment: optimized pricing

Results:
- Static Revenue: 11,839.60
- Optimized Revenue: 60,000.00
- Revenue Lift: 406.77%
- Statistically significant improvement (t-test)

---

## Technologies

Python · SQL · Prophet · SciPy · NumPy · Scikit-learn · Dynamic Programming · SQLite (Snowflake-style simulation) · Data Visualization

---

## Business Impact

This project demonstrates:

- End-to-end pricing pipeline from data warehouse to optimization
- Forecasting at appropriate aggregation levels
- Causal elasticity modeling
- Constrained revenue maximization
- Multi-period dynamic pricing
- Experimental validation of pricing strategies

The framework aligns with revenue management practices used in admissions pricing and large-scale consumer environments.
