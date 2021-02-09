# spotify-dataset
working with the [Kaggle Spotify Dataset 1921-2020, 160k+ Tracks dataset](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks)

## Overview
This project was used to predict the populatrity of a song based on various attributes. By guessing the average, a root mean squared error (RMSE) of 21.87 is achived. This is the baseline for the models to beat.

The current best algorithms are:
1. Random forest
  - RMSE: 12.591 (0.035)
2. DNN
  - RMSE: 13.56 (NA)
3. Linear Regression
  - RMSE: 17.172 (0.042)
4. Linear SVR
  - RMSE: 18.524 (0.088)

## Methods

### Data Exploration

### Model selection 

**Linear Regression** - RMSE: 17.172 (0.042)

![alt text](linear_reg.png)

**Random forest regression** - RMSE: 12.591 (0.035)

![alt text](rand_forest_reg.png)

**Linear SVR** - RMSE: 18.524 (0.088)

![alt text](svr.png)

**DNN** - RMSE: 13.56 (NA)

![alt text](DNN.png)

### Tuning Hyperparameters

### Generalization 
