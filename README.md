README: 

Sponsor: Benchmark Labs

Team Members:
Tarun Paravasthu, University of Rochester
Madeleine Johnson, University of Rochester
Brennan Kalinowski, University of Rochester
Sean Tian, University of Rochester

Project Description
This project aimed to improve short-term wave height forecasting at specific offshore locations, where accurate predictions can reduce weather-related delays and enhance operational planning for active and under-construction wind farms. The team evaluated several forecasting methods, including statistical models like ARIMA and advanced machine learning techniques such as XGBoost and Long Short-Term Memory (LSTM) neural networks to accomplish this. The dataset combined hourly buoy readings from NOAA’s National Data Buoy Center with historical weather data from the European Centre for Medium-Range Weather Forecasts (ECMWF) Reanalysis 5 ERA5 reanalysis project. The most effective approach was a hybrid Convolutional Neural Network (CNN) and LSTM model, which delivered highly accurate forecasts for 1–12 hour horizons, achieving accuracy scores up to 96% with minimal error. If deployed, this model, if implemented at only five offshore wind farms, could save up to $3.6 million annually by minimizing downtime caused by severe weather

Installation
We have uploaded the code to Box as well as a github repository with the following link: https://github.com/Tarun-Paravasthu/Point-Specific-Wave-Forecast/tree/main 

The code consists of 4 Jupyter Notebooks for accessing and processing NDBC and ERA5 data, and then running our forecasting models. We have also included the data csv file that we used for our final model evaluations, final_ndbc_data.csv



Files

Cdsapi_pipeline_and_data_preprocessing.ipynb
This file downloads and merges data from NDBC and ERA5 sources for selected locations and timeframes to create our final dataset. The required packages are pandas, numpy, cdsapi, xarray, and matplotlib.
NDBC data: 
download and clean NDBC data for selected stations and years
ERA 5 Data:
Download wave and meteorological data (e.g., swh, sst, mwp, ppld) from CDS using API 
Merge datasets into a unified, timestamped DataFrame:
Handle missing values and resample to uniform intervals
Save to CSV for model input

EDA.ipynb
This file uses the dataset created in the preprocessing file to run exploratory data analysis as well as our early SARIMA model testing. The required packages are pandas, matplotlib, statsmodels, and pmdarima (only used for auto-arima).
EDA:
Generates time series plot, summary statistics, histogram, and boxplot for wave height.
Time Series Analysis:
Generates ACF and PACF plots, as well as seasonal decomposition to understand seasonality
ARIMA:
Contains auto-arima as well as SARIMA model to generate a 12 hour forecast.

CNN_+_LSTM.ipynb
This notebook implements a hybrid Convolutional Neural Network (CNN) and Long Short-Term Memory (LSTM) model to forecast wave height at offshore locations using the most recent 24 hours of data to predict 6 hours into the future. The required packages are numpy, pandas, sci-kit learn, tesnsorflow, and matplotlib. The pipeline includes:
Data Preprocessing: The notebook loads and normalizes the dataset (final_ndbc_data.csv) using a MinMaxScaler. Sequences of 24 hours (input) are created to predict the 6th hour (target).
Model Architecture:
The CNN layer captures local temporal patterns in the time series data.
The LSTM layer then models long-term dependencies.
A final output layer outputs a single prediction.
Training & Evaluation:
The model is trained with early stopping based on validation loss.
RMSE is calculated for model evaluation.
The final model is plotted and evaluated using predictions vs. actual values across all forecast hours.

Model_testing.ipynb
This file contains a CNN+LSTM model and an XGBoost model for predicting 24 future hours based on the last 24 hours. The required packages are numpy, pandas, matplotlib, sklearn, tensorflow, and xgboost.
Data and Setup:
Using the same process as CNN+LSTM, creates X and y sequences of past values and future values to feed into a model.
Functions: 
Includes some functions to improve readability later in the code.
inv_transform: Inverse Transforms data after it has been scaled for interpretable results
get_error_df: Given predictions and actual values, creates a dataframe of error metrics by forecast hour
XGBoost: 
Contains XGBoost model training and evaluation.
CNN+LSTM: 
Contains CNN+LSTM model training and evaluation.
Comparison Plots: 
Plots error metrics from each model to compare results over forecast horizon. Also contains code to show example forecasts.

VMD__LSTM_V2.ipynb
This code is a work in progress, as we were not able to complete a rolling forecast to test the prediction accuracy of the VMD model due to data leakage explained in the report. However, we have included it as useful information for any future work. The required packages are pandas, numpy, math, matplotlib, vmdpy, tensorflow, and sklearn.
VMD component decomposition
Forecast with separate train and test data
Incomplete Rolling Forecast
Refer to this study for an explanation of the algorithm: https://www.frontiersin.org/journals/marine-science/articles/10.3389/fmars.2024.1382248/full 
