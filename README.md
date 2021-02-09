# Spotify Dataset
working with the [Kaggle Spotify Dataset 1921-2020, 160k+ Tracks dataset](https://www.kaggle.com/yamaerenay/spotify-dataset-19212020-160k-tracks)

## Overview
This project uses tool from Keras/TensorFlow, Scikit-Learn, Pandas, Numpy, TensorBoards, and Matplotlib to predict the populatrity of a song based on various attributes. 

By guessing the average of the data set for all songs, a root mean squared error (RMSE) of 21.87 is achived. This can be used a baseline to help understand model preformance.

The current best algorithms are:
1. Random forest - RMSE: 12.591 (0.035)
2. DNN - RMSE: 13.56 (NA)
3. Linear Regression - RMSE: 17.172 (0.042)
4. Linear SVR - RMSE: 18.524 (0.088)

## Methods
Prior to examining the data, duplicate rows were deleted and a testing set was set aside to be used later to measure how well the models generalize. 

### Data Exploration
The dataset contains 19 attributes and 172,230 unique entries. 4 of the attributes are text baised which are dropped, 1 is the label (popularity), and the remaining 14 are used as inputs to the models. They are:
- acousticness    
- danceability    
- duration_ms     
- energy          
- explicit        
- instrumentalness
- key             
- liveness        
- loudness        
- mode            
- popularity      
- speechiness     
- tempo           
- valence         
- year   

Looking at the correlation matrix, acousticness, energy, instrumentalness, loudness, and year are most correlated to popularity. The scatter matrix does not show any non linear correlations.

### Data Pipeline
The following text based attributes were dropped.
- 'artists'
- 'id'
- 'name'
- 'release_date'

The 'artists' attribute could be used via hot ones, but this would lead to a large number of input parameters. The dataset also has a 'year' attribute making 'release_data' somewhat redundent. 

After the text attributes were remove, the data was passed through sklear-learn's standard scaler to normalize the data.

### Model selection 
Model were given the cleaned data and run with the default hyperparameters. 3 Fold cross validation was used to get preformance (except on DNN), and a single fold was used to show the prediction vs expected error plots. The best models were then used for hyperparameter tuning.

#### Linear Regression - RMSE: 17.172 (0.042)
The results for linear regression were not much better than guessing the average. It is likely that the data is not linearly seperable.

![alt text](linear_reg.png)


#### Random forest regression - RMSE: 12.591 (0.035)
The random forest model preformed the best for initial testing. Could still use some work. 

![alt text](rand_forest_reg.png)

#### Linear SVR - RMSE: 18.524 (0.088)
The linear SVR had the worst performance of all models. It looks to be due to over prediction the popularity of unpopular songs. The clear seperation on the left side of the graph suggests the data is not linearly seperable. Using a different kernel might help, but SVR is likely not a good choice.

![alt text](svr.png)

#### Deep Neural Network (DNN) - RMSE: 13.56 (NA)
The DNN used for testing had 2 hidden layers with 30 nodes and a single output layer for the regression. The preformance of the training data vs validation data suggests overfitting, but the model prefomed well in comparison to others. 

![alt text](DNN.png)

### Tuning Hyperparameters
For Hyperparameter tuning, I went with Random Forest and DNN models. Below are how I tuned the hyperparameters

#### Deep Neural Network (DNN)
The DNN was trained using Keras/TensorFlow and the training was monitored with a TensorBoard. The first round of tuning was a grid search with the number of hidden layers = [1, 2, 3], neurons per layer = [30, 100, 200], and learning rate = [1e-3, 1e-4, 1e-5]. The best model was 3 hidden layers, 200 neurons per layer and a learning rate of 1e-4 with a RMSE=13.055. 

However, the large seperation between the training loss and validation loss suggest all models were overfitting. Therefore I simplified the model with the second grid search: the number of hidden layers = [1, 2, 3], neurons per layer = [10, 20, 30], and learning rate = [1e-3, 1e-4, 1e-5]. 

next up try activation='selu', kernel_initializer='lecun_normal'

#### Random forest regression

### Generalization 

### Summary and Outlook

