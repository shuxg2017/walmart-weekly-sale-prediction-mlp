# Walmart Weekly Sale Prediction By Neural Network

### In this project, I used univariate ARIMA or univariate LSTM to forecast Walmart weekly sale, but the performances were very poor. Therefore, I moved to multivariate model. The image below was my final result. The model was pretty powerful, it can predict weekly sales in any stores with any departments.

![Final Result](https://github.com/shuxg2017/Walmart-weekly-sale-prediction-by-MLP/blob/master/results/result.png)

## Introduction

I trained a very simple neural network (fully connected layers) to predict Walmart weekly sale. Before training the model, I did data integration and feature engineering. In addition, I searched the same work which were done by other machine learning engineers. The metrics they used were mean absolute error (MAE). Achieving MAE below 2000 will be a good result.
 **Goal: reduce the MAE below 2000.**

### Data Overview

Total Observations | 60% Train | 20% Valid | 20% Test
-------------------|-----------|-----------|----------
421,570 | 252,942 | 84,314 | 84,314

- The image below shows overall weekly sales across 45 stores in the time order.
  - Black dots: Black Fridays.
  - Blue dots: Pre Christmas days
  - Actual Christmas: there were the steepest drops.

![TimeSeries](https://github.com/shuxg2017/Walmart-weekly-sale-prediction-by-MLP/blob/master/results/Overall_Weekly_Sale.png)

### Result Overview

**We achieved MAE 1677!!!**

Model Structure | # of params | Other Techniques | Data Increment | Train MAE | Validation MAE | Test MAE | Result
----------------|-------------|------------------|----------------|-----------|----------------|----------|--------
32/16/8/1 | 5,889 | None | 0 | 1790 | 1819 | 1811 | Poor performance on Black Friday and Pre Christmas
64/32/16/8/1 | 13,185 | Oversampling Black Friday (repeat 10 times) & Pre Christmas (2 times) | Black Friday: 16,128 & Pre Christmas: 10,710 | **1636** | **1679** | **1677** | Best MAE, no overfitting


### Feature Engineering

![EncodedSpecialDays](https://github.com/shuxg2017/Walmart-weekly-sale-prediction-by-MLP/blob/master/results/OneHotEncodeExample.png)

**Remapping 15 original features into 162 features.**

- Originial features per observation (15 features)
  - Store
  - Dept
  - Store Type
  - Store Size
  - Date
  - IsHoliday
  - Temperature
  - Fuel_Price
  - MarkDown 1 ~ 5 
  - Consumer Price Index
  - Unemployment
- After feature engineering (162 features)
  - One hot encode
    - Store
    - Dept
    - Store Type
    - Month
    - Black Friday or not Black Friday
    - Christmas coming soon or not coming soon
    - Christmas just ended or not
    - IsHoliday
    - Temperature: cold, cool, warm, mild, hot
    - MarkDown: present or not present
  - Remove Store Size
  - Untouched
    - Fuel_Price
    - Consumber Price Index
    - Unemployment
  - New added
    - Median weekly price of each Store with each Dept
