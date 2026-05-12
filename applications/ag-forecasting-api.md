# 🌾 Agricultural Forecasting API

FastAPI-based ASGI service for crop disease risk forecasting using multi-source weather data, developed by the University of Wisconsin–Madison Data Science Institute and integrated with Open-Lambda technology.

---

## Overview

The API provides geospatial agricultural intelligence for Wisconsin, combining weather data with validated crop disease forecasting models.


## Setup

```bash
git clone https://github.com/UW-Madison-DSI/ag_forecasting_api.git
cd ag_forecasting_api

python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt

uvicorn app:app --reload
```