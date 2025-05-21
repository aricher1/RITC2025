# RITC2025
Rotman International Trading Competition Python Scripts
# Commodities News Trading Script – RITC 2025

A Python-based trading script built for the **Refiner role** in the **Rotman Interactive Trading Competition (RITC) 2025**. This tool parses real-time news articles related to **Heating Oil (HO)** and makes automated trading decisions based on quantitative analysis provided by the competition’s framework.

**Author**: Aidan Richer  
**Year**: 2025

---

## Overview

This script listens for breaking news related to Heating Oil, extracts relevant data using regular expressions, calculates an expected closing price using the RITC-provided pricing model, and issues a trading signal (long or short) based on the delta between current and predicted price.

---

## Features

- Real-time integration with RIT API
- Automatic parsing of temperature-related market news
- Dynamic calculation of expected price changes
- Clear trading signals: **Long** or **Short**
- Lightweight and fast main loop with deduplication of articles

---

## How It Works

1. **Checks if the case is active** using the `/v1/case` endpoint.
2. **Pulls the latest news article** using the `/v1/news` endpoint.
3. **Parses the article** for:
   - Expected vs. Realized Weekly Temperatures
   - Standard Deviation of Weekly Temperature
   - Current Price of Heating Oil
   - Any percentage-based adjustment hints
4. **Calculates expected final price** using:
   ```python
   final_price = current_price + (expected_temp_change / std_dev)
   final_price *= (1 + percentage_change)
