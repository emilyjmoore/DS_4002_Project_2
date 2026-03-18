# Charlottesville Housing Price Forecasting with Sentiment Analysis

## Overview

This project examines whether incorporating textual sentiment from Housing Advisory Committee (HAC) meeting minutes improves forecasts of Charlottesville housing prices compared to a baseline time-series model. The analysis compares a traditional ARIMA model with an extended ARIMAX model that includes sentiment-based features derived from meeting minutes.

The analysis compares:
* A baseline ARIMA model using only historical housing price data
* An extended ARIMAX model that includes sentiment features derived from meeting minutes


## Map of Documentation 

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


## Section 2: Instructions for Reproducing Results

Follow these steps to reproduce the results of this project:

### Step 1: Set Up Environment

1. Install Python (version 3.8 or higher recommended)
2. Install required packages:

```bash
pip install pandas numpy pdfplumber nltk statsmodels pmdarima
```

3. Download NLTK tokenizer (only needed once):

```python
import nltk
nltk.download('punkt')
```


### Step 2: Prepare Data

1. Place all housing market report PDFs into the `data/` folder
2. Place all HAC meeting minutes PDFs into the appropriate folder used in your scripts


### Step 3: Extract Housing Data

Run the script:

```bash
python scripts/scrape_caar_data.py
```

This will:

* Extract median price, sales volume, and price change percentage
* Save the output as `caar_data.csv`


### Step 4: Process Meeting Minutes

Run:

```bash
python scripts/process_meeting_minutes.py
```

This will:

* Extract text from PDFs
* Count housing and uncertainty-related words
* Compute total word counts
* Generate sentiment-related variables
* Save output as `housing_uncertainty_with_score.csv`


### Step 5: Merge Datasets

Run:

```bash
python scripts/merge_datasets.py
```

This will:

* Combine housing and sentiment datasets
* Remove unnecessary columns (e.g., file names)
* Compute:

  * `median_price_change_pct`
  * `sentiment_score`
* Save final dataset as `combined_housing_sentiment.csv`


### Step 6: Run Modeling

Open and run:

```bash
notebooks/analysis.ipynb
```

This notebook will:

* Load the final dataset
* Fit an ARIMA model (baseline)
* Fit an ARIMAX model (with sentiment variables)
* Generate forecasts
* Compute evaluation metrics (RMSE and MAE)


### Step 7: Compare Results

* Compare RMSE and MAE from both models
* Determine whether sentiment improves predictive accuracy


## Expected Outcome

If the hypothesis is correct:

* The ARIMAX model will produce lower RMSE and MAE than the ARIMA model
* Sentiment variables will improve out-of-sample forecasts

