---
blogpost: true
date: 2026-05-18
author: Maria Oros, Tyler Caraza-Harter
category: Case Studies
tags: case-study, agforecast, asgi, fastapi, openlambda
language: en
---

# An Application Case Study: Forecasting Crop Disease with OpenLambda

*Maria Oros, Data Science Institute, University of Wisconsin–Madison*  
*Tyler Caraza-Harter, Department of Computer Sciences, University of Wisconsin–Madison*

Our goal is to make an ever-growing set of applications deployable on OpenLambda (OL), with minimal modifications. We believe the best way to work towards this goal is to pick interesting applications that weren't originally designed for serverless deployment, try to port them to OL, and identify pain points. This helps us identify the most useful features to add to OL, to support similar deployments.

Recently, we selected an agricultural forecasting application (AgForecast), developed by the [Data Science Institute at UW–Madison](https://dsi.wisc.edu/), to port to OpenLambda: <https://github.com/UW-Madison-DSI/ag_forecasting_api>. AgForecast is an interesting case study, because it implements its REST API using FastAPI, which in turn uses [ASGI](https://asgi.readthedocs.io/en/latest/), the so-called "spiritual successor" to WSGI, which we recently started supporting in OpenLambda. WSGI is the basis for popular Python web-programming packages such as Django and Flask; new ASGI support opens the door to an even broader range of applications.

In this post, we describe the challenges of porting AgForecast to OL, and four new features we added to OL to make deployment of similar applications in the future simpler. The features are built-in ASGI support, direct GitHub-to-OL deployments, OL function environment variables, and OL-based pip compilation.