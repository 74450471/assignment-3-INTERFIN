# assignment-3-INTERFIN
please, see the Jupyter Notebook documentation in the file section of the repository

The code was outsourced from https://towardsdatascience.com/forecasting-exchange-rates-using-arima-in-python-f032f313fc56

However, I had to change parts of the code adapting it to Python (python 3.11). See the changes below 

1)Because there is no disp() argument in Python 3.11, I had to define the function like this (chapt GPT helped me in this): 

def StartARIMAForecasting(Actual, p, d, q):
	model = ARIMA(Actual, order=(p, d, q))
	model_fit = model.fit()
	prediction = model_fit.forecast()[0]
	return prediction 

2)I have then defined the for loop function (the one that iterates over the data and stores the values in separate variables) like this: 

for timepoint in TestData.index:
    ActualValue = TestData.loc[timepoint, "Price"]
    # forecast value
    Prediction = StartARIMAForecasting(TestData['Price'].values, 3, 1, 0)
    print('Actual=%f, Predicted=%f' % (ActualValue, Prediction))
    # add it to the list
    Predictions.append(Prediction)
    Actual.append(ActualValue)

3)Then I had to change the matplotlib to plot the forecast values. In the original version, the plot has not been sourcing the data from proper variables,i.e. predictions from predictions and actual from actual 

import matplotlib.pyplot as plt
import pandas as pd

TestData["Date"] = pd.to_datetime(TestData["Date"])

plt.plot(TestData["Date"], TestData["Price"])
plt.plot(TestData["Date"], Predictions, color='red')
plt.show()
