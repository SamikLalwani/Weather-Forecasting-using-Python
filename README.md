# Weather-Forecasting-using-Python
Data science has a wide range of applications, from which studying of weather is a sub-topic. With the help of various refernces I have attempted to create a small project depicting the principles of data science (PDS). 

In Data Science, weather forecasting is an application of Time Series Forecasting where we use time-series data and algorithms to make forecasts for a given time. If you want to learn how to forecast the weather using your Data Science skills, this article is for you. In this article, I will take you through the task of weather forecasting using Python step by step.

Weather forecasting is the task of forecasting weather conditions for a given location and time. With the use of weather data and algorithms, it is possible to predict weather conditions for the next 'n' number of days. For forecasting weather using Python, we need a dataset containing historical weather data based on a particular location. Here we are using a dataset from Kaggle based on the Daily weather data in New Delhi. ( You can access the dataset used in this porject from provided resources in this repo)

To begin with, we need to import all the necessary libraries and the data set that we will be using in this mini project:

```Python

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import plotly.io as io
io.renderers.default='browser'

data = pd.read_csv("E:\DailyDelhiClimateTrain.csv")

```
Here the path link needs to be changed according to you depending on where you have saved your data set. Copy the file path and replace it with the path on the line having data = pd.read_csv("E:\DailyDelhiClimateTrain.csv"). We have used our default renderer as browser, this is where your graphs/plots will be displayed.

Now, we will test whether the data has been successfully imported into your code:
```Python

print(data.head())
print(data.describe())
print(data.info()) ## Displays the type of data (such as int, float, etc)

```
Now, we will display the mean temperature, the humidity, and the wind speed with the help of plotly.express library. We will be displaying the data in form of a line graph. We will also provide respective titles to each graph.

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

With the help of plotly express we can also display a comparison between the two coloumns of a data set. For instance lets check the relationship between the Mean temperature and the Humidity. To do this we can write our code like this:

```Python

#%% Relation between temp and humidity
figure = px.scatter(data_frame = data, x="humidity",
                    y="meantemp", size="meantemp",
                    trendline="ols",
                    title = "Relationship Between Temperature and Humidity")
figure.show()


```
Moving on, for understanding weather and forecast it properly, we need to compare weather change over the years. This can be done with the help of the seaborn library. You can learn more about seaborn from https://www.geeksforgeeks.org/introduction-to-seaborn-python/. We will write our code as follows:

```Python

#%% Temp change in delhi over the years
plt.style.use('fivethirtyeight')
plt.figure(figsize=(15, 10))
plt.title("Temperature Change in Delhi Over the Years")
sns.lineplot(data = data, x='month', y='meantemp', hue='year')
plt.show()

```

Run your code and your data should be displayed in this way:
![image](https://user-images.githubusercontent.com/71218661/229753025-9c88a868-ebd3-4b69-b85a-86ee1e515430.png)

Now we will be using the Prophet model to display a forecast plot. What is Prophet model:
Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data. Since the weather is a time series data, using Prophet is the best fit.

```Python

#%% Changing data column names to ds and y for prophet
forecast_data = data.rename(columns = {"date": "ds",
                                       "meantemp": "y"})
print(forecast_data)

```
Using the above code we can change the column names to 'ds' and 'y', as Prophet model only accepts the data labeled as 'ds' and 'y'. Run the section and you should notice that the column labeled date has been chnaged to 'ds' and the meanteamp has been changed to 'y'.

![image](https://user-images.githubusercontent.com/71218661/229754519-db9db3cb-0c76-4e53-b257-7025023bae8b.png)

```Python

#%% Using Prophet Model for forecast

from prophet import Prophet
from prophet.plot import plot_plotly, plot_components_plotly

model = Prophet()
model.fit(forecast_data)

forecasts = model.make_future_dataframe(periods=365)
predictions = model.predict(forecasts)
plot_plotly(model, predictions)

```
Lastly run the above code and you will get a forecast plot like this:
![image](https://user-images.githubusercontent.com/71218661/229754718-9f82011c-0d64-4610-9e98-ecb13ed60724.png)

However, this is what I have tried with the help of references and by understanding its concepts. I want to build more around this project and maybe try it with other data sets. I would love to take advice to improve my project and make it more reliable and efficient. Please do suggest changes if you can. Thank You!
