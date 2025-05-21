# SurfacePredictor
This project focuses on developing machine learning models to identify different surface types using time-series data collected from a pressure sensor. The goal is to classify surfaces such as Glass, Paper, Marble, and others by analyzing their resistance patterns over time.

This project focuses on developing machine learning models to identify different surface types using time-series data collected from a pressure sensor. The goal is to classify surfaces such as Glass, Paper, Marble, and others by analyzing their resistance patterns over time.

Project Highlights
Data Cleaning & Preprocessing:
Removal of invalid or empty columns, handling missing data, and normalization of sensor readings.

Feature Engineering:
Extraction of statistical features (mean, max, min, standard deviation, energy, slope, etc.) from resistance time series to capture surface characteristics.

Modeling Approaches:

Random Forest Classifier for baseline surface recognition, including binary classification experiments for individual surfaces.

LSTM-based deep learning model to capture temporal dependencies in sensor data for improved classification accuracy.

Visualization & Interpretability:

PCA and t-SNE visualizations to explore feature separability.

Feature importance analysis from Random Forest to identify key contributing features.

Inference on Unseen Data:
Demonstrated model ability to classify new, unseen samples from sensor data.
