# Weather-Forecasting-using-Python
Data science has a wide range of applications, from which studying of weather is a sub-topic. With the help of various refernces I have attempted to create a small project depicting the principles of data science (PDS). In Data Science, weather forecasting is an application of Time Series Forecasting where we use time-series data and algorithms to make forecasts for a given time. If you want to learn how to forecast the weather using your Data Science skills, this article is for you. In this article, I will take you through the task of weather forecasting using Python step by step.

Weather forecasting is the task of forecasting weather conditions for a given location and time. With the use of weather data and algorithms, it is possible to predict weather conditions for the next 'n' number of days. For forecasting weather using Python, we need a dataset containing historical weather data based on a particular location. Here we are using a dataset on Kaggle based on the Daily weather data in New Delhi.

First we need to import all the necessary libraries and the data set that we will be using in this mini project:

```Python

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import plotly.io as io
io.renderers.default='browser'

data = pd.read_csv("E:\DailyDelhiClimateTrain.csv")

```
Here the path link needs to be changed according to you, depeneding on where you have saved your data set. Copy the file path and replace it my path on the line having 
data = pd.read_csv("E:\DailyDelhiClimateTrain.csv"). We have used our default renderer as browser, this is where your graphs/plots will be displayed.

Now, we will test whether the data has been successfully imported into your code:
```Python

print(data.head())
print(data.describe())
print(data.info()) ## Displays the type of data (such as int, float, etc)

```
Now, we will display the mean temperature, the humidity and wind speed with the help of plotly.express library. We will be displaying the data in form of a line graph.

```Python

#%% Mean temp in Delhi
figure = px.line(data, x="date",
                 y="meantemp",
                 title='Mean Temperature in Delhi Over the Years')
figure.show()

#%% Humidity in Delhi
figure = px.line(data, x="date",
                 y="humidity",
                 title='Humidity in Delhi Over the Years')
figure.show()

#%% Wind speed in delhi
figure = px.line(data, x="date",
                 y="wind_speed",
                 title='Wind Speed in Delhi Over the Years')
figure.show()

```
The data should look something like this:
![image](https://user-images.githubusercontent.com/71218661/229749452-49400c66-18a2-4a5a-9b34-a5b7a81abeba.png)

With the help of plotly express we can also display a comparison bewteen two coloums of a data set. For instance lets see the relationship between the Mean temperature and the Humidity. To this we can write our code like this.

```Python

#%% Relation between temp and humidity
figure = px.scatter(data_frame = data, x="humidity",
                    y="meantemp", size="meantemp",
                    trendline="ols",
                    title = "Relationship Between Temperature and Humidity")
figure.show()


```


We will be using the Prophet model. What is Prophet model:
Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data. Since weather is a time series data, using prophet is the best fit.

