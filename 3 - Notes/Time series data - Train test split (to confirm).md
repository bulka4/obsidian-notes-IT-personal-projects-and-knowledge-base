Tags: [[__Machine_Learning]]
#MachineLearning 

# Introduction
Those notes should be verified, I am not sure if they are correct.

When performing train test split for time series data, usually it is better to include in both train and test datasets one continuous timeframe rather then mix them.

For example, if we have data for 12 months, it is usually better to include months 1-10 in the training dataset and months 11-12 in the testing one rather then use months 3 and 7 for testing.

