# Charlottesville Housing Price Forecasting with Sentiment Analysis

## Overview

This project examines whether incorporating textual sentiment from Housing Advisory Committee (HAC) meeting minutes improves forecasts of Charlottesville housing prices compared to a baseline time-series model. The analysis compares a traditional ARIMA model with an extended ARIMAX model that includes sentiment-based features derived from meeting minutes.

The analysis compares:
* A baseline ARIMA model using only historical housing price data
* An extended ARIMAX model that includes sentiment features derived from meeting minutes

---

```
PROJECT/
│
├── DATA/
│   ├── caar_monthly_housing_reports
│       ├── 25-03-caar-market-indicators.pdf
│       ├── 25-04-market-report.pdf
│       ├── 25-05-market-indicator-report.pdf
│       ├── 25-06-market-indicator-report.pdf
│       ├── 25-07-market-indicator-report.pdf
│       ├── 25-08-market-indicators-report.pdf
│       ├── 25-09-market indicator-report.pdf
│       ├── 25-10-market-report.pdf
│       └── 25-11-market-report.pdf                      
│   ├── cville_housing_advisory_meeting_mins
│       ├── HAC Minutes_03-19-2025.pdf
│       ├── HAC Minutes_04-16-2025.pdf
│       ├── HAC Minutes_05-21-2025.pdf
│       ├── HAC Minutes_06-18-2025.pdf
│       ├── HAC Minutes_07-16-2025.pdf
│       ├── HAC Minutes_09-17-2025.pdf
│       ├── HAC Minutes_10-15-2025.pdf
│       ├── HAC Minutes_11-12-2025.pdf
│       └── HAC Minutes_12-17-2025.pdf
│   └── Data Appendix.pdf     
│
├── SCRIPTS/ 
│   ├── scrape_meeting_data.ipynb
│   ├── scrape_caar_data.ipynb  
│   ├── join_csv_files.ipynb
│   ├── price_change_vs_sentiment_dual_plot.ipynb
│   ├── sales_volume_vs_price_dual_plot.ipynb
│   ├── median_housing_line_plot.ipynb
│   ├── uncertainty_score_line_plot.ipynb
│   └── time_series_model.ipynb
│
├── OUTPUT/
│   ├── anaconda_projects_70fc63d5-d421-4385-b8bd-8b35803e6016_median_price_over_time.png
│   ├── anaconda_projects_70fc63d5-d421-4385-b8bd-8b35803e6016_price_change_vs_sentiment.png
│   ├── anaconda_projects_70fc63d5-d421-4385-b8bd-8b35803e6016_sales_volume_vs_price.png
│   ├── anaconda_projects_70fc63d5-d421-4385-b8bd-8b35803e6016_uncertainty_over_time.png
│   ├── caar_data.csv
│   ├── combined_housing_sentiment.csv
│   ├── housing_uncertainty.csv
│   └── housing_uncertainty_with_score.csv                
│
└── README.md                             
```

---

## Section 1: Software and Platform

### Software Used

* Python (primary programming language)
* Jupyter Notebook (for analysis and modeling)

### Required Python Packages

The following libraries are required to run the project:

* pandas
* numpy
* pdfplumber
* nltk
* statsmodels
* pmdarima
* re (built-in)
* os (built-in)

You can install the required packages using:

```
pip install pandas numpy pdfplumber nltk statsmodels pmdarima
```

### Platform

This project was developed and tested on:

* macOS (Mac)

It should also run on:

* Windows
* Linux

---

## Data Sources

### Housing Market Data

Monthly housing reports containing:

* Median sales price
* Sales volume
* Price change percentage

### HAC Meeting Minutes

* PDF documents of meeting minutes
* Converted to text and processed for sentiment analysis

---

## Methodology

### Data Extraction

* Housing data extracted using regex from PDF reports
* Meeting minutes processed using NLP techniques

### Feature Engineering

* Word counts and keyword frequencies calculated
* Sentiment score computed as:

```
sentiment_score = (housing_mentions - uncertainty_mentions) / minutes_word_length
```

* Dates extracted from filenames and standardized to `YYYY-MM`
* Lagging applied so sentiment at time *t* predicts price at *t+1*

### Modeling

* Baseline: ARIMA (price only)
* Extended: ARIMAX (price + sentiment variables)

### Evaluation

Models are evaluated using:

* RMSE (Root Mean Squared Error)
* MAE (Mean Absolute Error)

---

## Expected Results

The ARIMAX model is expected to outperform the ARIMA model if sentiment contains predictive information about future housing prices.

---


Emily Moore
