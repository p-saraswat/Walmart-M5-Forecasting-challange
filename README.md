# M5 Forecasting
#### Estimate the unit sales of Walmart retail goods

### Project Description
This project presents hierarchical sales data from Walmart, the world’s largest company by revenue. The aim is to forecast daily sales for the next 28 days. The data, covers stores in three US States (California, Texas, and Wisconsin) and includes item level, department, product categories, and store details. In addition, it has explanatory variables such as price, promotions, day of the week, and special events. Together, this robust dataset can be used to improve forecasting accuracy.

### Problem Statement
Walmart wants to know the accurate point forecasts for the upcoming 28 days of sale. 

#### Point forecasts:
The accuracy of the point forecasts will be evaluated using the Root Mean Squared Scaled Error (RMSSE), which is a variant of the well-known Mean Absolute Scaled Error (MASE).


### About the Dataset
M5 is a Walmart dataset about products sold in the stores of USA. It has a grouped time series format. Data involves unit sales of 3,049 products, classified in 3 product categories (Hobbies, Foods, and Household) and 7 product departments, in which the above-mentioned categories are disaggregated. The products are sold across ten stores, located in three States (CA, TX, and WI). The time range of dataset is from 2011-01-29 to 2016-06-19. The dataset consists of the following 3 tables:
1. Calendar: Contains information about the dates the products are sold
2. Sell prices: Contains information about the price of the products sold per store and date
3. Sales train: Contains the historical daily unit sales data per product and store

Please see the below illustration for details:
![image.png](levels.png)

### Approach Summary
We started with a high level data exploration of M5 dataset to understand details and variation. Then we did feature engineering to create features on a product sale level. The features included defining lags, rolling means and SNAP program details. Then we used different Hierarchy of data set for modelling based on stores, departments and categories in the dataset.
We tried to use Neural Networks as well as Ensemble Tree-based Regressors at many different levels. The results for the best models (several others were experimented with but were not trained fully as the initial results were subpar)used were as follows:
| Model Name | Model Hierarchy Level | Total Number of Models | Model Score |
|---|---|---|---|
| LightGBM | Per Store | 10 | 0.6229 |
| XGBoost | Per Store | 10 | 0.6211 |
| GRU | Per Store | 10 | 0.8026 |
| Wavenet | Per Store | 10 | 16.7120 |
| LSTM | Per Store | 10 | 0.9430 |
| LightGBM | Per Store Per Category | 30 | 0.6292 |
| LightGBM | Per State Per Category | 30 | 0.64231 |
| LightGBM | Per Department | 10 | 2.138 |
| __LightGBM__ | __Per Store Per Department__ | __70__ | __0.52978__ |
<!-- ![table.png](table.png) -->

1. Store-wise level models: RNN, LSTM, GRU, Wavenet, XGB and LGBM
2. Department-wise level models: LGBM
3. State and category-wise level model: LGBM
4. Store and category-wise level model: XGBoost and LGBM
5. Store and Department-wise level: LGBM

After creating these models and tuning the best hyperparameters for them, we made the forecast prediction of future sales of 28 days with an WRMSSE of __0.52978__.

![image](./final_result.jpeg "Best Kaggle Private Score")