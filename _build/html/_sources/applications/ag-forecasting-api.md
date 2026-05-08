# 🌾 Agricultural Forecasting API

FastAPI-based service for **crop disease risk forecasting** and **winter rye biomass estimation** using multi-source weather data.  
Developed by the University of Wisconsin–Madison Data Science Institute.

---

## Overview

The API provides geospatial agricultural intelligence for Wisconsin, combining weather data with validated agronomic models.

### Key Features
- 🌽 Crop disease risk forecasting (corn & soybean)
- 🌱 Winter rye biomass estimation
- 🌦 Multi-source weather integration (IBM EIS, WiscoNet, NOAA)
- 📍 Coordinate and station-based queries
- 🗺 GeoJSON outputs for GIS applications
- ⚡ Async batch processing for multi-station analysis

---

## System Architecture

The system is structured into four main layers:

- **API Layer (FastAPI)**  
  Handles incoming requests and routing (`/ibm`, `/wisconet_g`, `/models`)

- **Data Layer**  
  - IBM EIS: high-resolution global weather API  
  - WiscoNet: Wisconsin mesonet station network  

- **Processing Layer**  
  Weather normalization, unit conversion, GDD calculation, rolling features

- **Model Layer**  
  Disease risk models and winter rye biomass model

---

## Core Modules

- Weather ingestion (IBM + WiscoNet)
- Disease risk modeling
- Winter rye biomass estimation
- Async pipeline orchestration
- GeoJSON response formatting

---

## API Endpoints

### IBM Forecasting (Coordinates)
`GET /v2/ag_models_wrappers/ibm`

Returns disease risk + biomass using IBM weather data.

---

### WiscoNet Forecasting (Stations)
`GET /v2/ag_models_wrappers/wisconet_g`

Returns station-based time-series disease risk and biomass.

---

### Model Metadata
`GET /v2/ag_models_wrappers/models`

Returns available disease and biomass models.

---

## Disease Models

- **Tarspot (corn)** – humidity and temperature-based risk
- **Gray Leaf Spot (corn)** – temperature + dew point model
- **Frogeye Leaf Spot (soybean)** – GDD + rainfall model
- **White Mold (soybean)** – precipitation and soil moisture model

---

## Winter Rye Biomass Model

Predicts dry biomass (lb/acre) using:

- Growing Degree Days (0°C base)
- Planting date (day-of-year)
- Fall precipitation
- Logistic growth curve

### Outputs
- Biomass (lb/acre)
- Color class (gray / yellow / green)
- Interpretation message

---

## Data Sources

### IBM Environmental Intelligence Suite (EIS)
- High-resolution global weather data
- Hourly forecasts and historical data
- Requires authentication

### WiscoNet
- Wisconsin mesonet (~100 stations)
- Daily weather observations
- Public API access

---

## Response Format

All outputs are returned as **GeoJSON FeatureCollections**, including:

- Weather variables
- Disease risk scores
- Biomass predictions
- Station metadata

---

## Performance Features

- Async multi-station processing
- Cached weather and station data (6h–7d TTL)
- Parallel risk computation
- Optimized data aggregation pipeline

---

## Setup

```bash
git clone <repo>
cd ag_forecasting_api

python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt

uvicorn app:app --reload
```