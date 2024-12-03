# Conversionista Forecast Data Pipeline

## Overview

This Dataform project manages the data pipeline for Conversionista's forecasting system. It integrates data from various sources, processes it through multiple layers, and produces aggregated forecast data for analysis and reporting.

## Data Sources

- **src_forecast_se dataset:**
  - `people`
  - `assignments`
  - `projects`
  - `clients`

- **src_forecast_no dataset:**
  - `people`
  - `assignments`
  - `projects`
  - `clients`

- **stg_happy_people dataset:**
  - `employees` table

- **Public holidays:** Fetched from an existing spreadsheet

Data from the forecast datasets (SE and NO) is implemented as views due to limitations in changing table names when defining a source through `definition`.

## Data Layers

### Source Layer (`src_layer`)

Raw data from the above mentioned sources. 

### Staging Layer (`stg_layer`)

- Merged data tables (Swedish + Norwegian) filtered for Conversionista employees
- Includes `forecast_full` and `forecast_daily`

### Aggregated Layer (`agg_layer`)

- `forecast_daily`: Forecast data per employee per day
- `forecast_per_week`: Weekly aggregation
- `forecast_per_month`: Monthly aggregation

## Key Tables

1. `int_harvest_forecast`: Integrated forecast data
2. `stg_forecast_daily`: Daily forecast data 
3. `int_forecast_daily`: Forecast data per employee per day
3. `int_forecast_per_week`: Weekly aggregated forecast
4. `int_forecast_per_month`: Monthly aggregated forecast

## Configuration

The project currently uses a single dataset for all tables:

```json
{
  "defaultSchema": "c_forecast_dev",
  "assertionSchema": "dataform_assertions"
}

Additional variables are in workflow_settings.yaml that can be changed if project requires.


