# CS4347.R02
Avocado Price Prediction Project

## **1\. Project Overview & Goals**

This project utilizes machine learning and time-series forecasting techniques to predict the average price of conventional avocados in the United States. The goal was to determine the most effective modeling approach for short-term price forecasting in a volatile agricultural market.

We analyzed the "Avocado prices" dataset sourced from the Hass Avocado Board via Kaggle. We compared three distinct models using a one-step-ahead rolling forecast methodology:
1. **Baseline ARIMA (p = 0, d = 1, q = 0)**
2. **Seasonal ARIMA (p = 0, d = 1, q = 0), (p = 0, d = 0, q = 1)[s = 52]**
3. **Facebook/Meta's Prophet**

## **2\. Repository Structure**

The project is organized as follows:  
Project/  
├── ARIMA\_Graph.png         \# Visualization of ARIMA vs. Actuals  
├── Prophet1\_Graph.png      \# Initial Prophet Static Forecast  
├── Prophet2\_Graph.png      \# Prophet Rolling Forecast  
├── README.md               \# Project documentation  
└── Code & Data/  
    -----├── avocado.csv         \# Original dataset  
    -----├── AvocadoPrices.ipynb \# Main Jupyter Notebook containing all analysis  
    -----└── requirements.txt    \# Python dependencies

## **3\. Setup & Installation**
### **Option 1: Local Setup**

1. Clone or download this repository
2. Navigate to Code & Data directory
3. Install the required dependencies
(It is recommended that you create a virtual environment to install the dependencies into)   
   ```pip install -r requirements.txt```
4. Launch Jupyter Notebook:
   ```jupyter notebook "AvocadoPrices.ipynb"```
### **Option 2: Google Colab**
1. Upload "AvocadoPrices.ipynb" and "Avocado.csv" to your Google Colab session.
2. Install necessary libaries at the top of the notebook if they are not preinstalled
        
## **4\. Dependencies**
The project relies on the following libraries; See "requirements.txt" for exact versions (Python 3.12)   
   * pandas: Data manipulation and time-series handling.

   * numpy: Numerical computations.

   * matplotlib / seaborn: Data visualization.

   * statsmodels: For ARIMA implementation and statistical tests (ADF, ACF/PACF).

   * pmdarima: For the auto_arima function to find optimal parameters.

   * prophet: For the Facebook Prophet forecasting model.

   * scikit-learn: For evaluation metrics (MAE, RMSE, R²).

## **5\. Methodology & Assumptions**
### **Data Assumptions**
   * **Scope:** The analysis is strictly limited to the "**TotalUS**" region and "**conventional**" avocado type
   to ensure a consistent, high-volume time series.
   * **Frequency:** Data is aggregated on a weekly basis
   * **Stationarity:** The raw price was non-stationary; a first-order difference (*d* = 1) was applied to stablize the mean.
### **Forecasting Methodology**
A portion of this project focuses on the difference between *Static* and *Rolling* forecasts
   * **Static Forecast:** Training on data up to 2017 and predicting the next 25 weeks blindly (base run for Prophet)
   * **Rolling Forecast(One-Step-Ahead):** The model predicts one week (i + 1), learns the actual value from that week, re-trains, and then predicts i + 2.
