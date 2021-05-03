# rate-of-return-calculator
Calculates Simple and Log rates for any symbol in yahoo finance. 

Calculating the Rate of Return of DOGE coin using Python
Disclaimer: This is for educational purposes only and not financial advice.
Recently we have seen all over the internet and in real life an explosion of the DOGE coin phenomena. It is on a steady climb up, reaching new highs. As of writing this article, the price of 1 DOGE coin is $0.383291, But would it have been a good investment if you had got in earlier? We will find out using a rate of return calculator written in python.
You can get the Jupyter notebook here.
What is an Average Rate of Return?
According to Investopedia, A rate of return (RoR) is the net gain or loss of an investment over a specified time period, expressed as a percentage of the investment's initial cost. When calculating the rate of return, you are determining the percentage change from the beginning of the period until the end.
The rate of return (RoR) is used to measure the profit or loss of an investment over time.
The metric of RoR can be used on a variety of assets, from crypto to stocks.
The effects of inflation are not considered in the simple rate of return calculation or the logarithmic rate return. Still, they are in the real rate of return calculation.

The source code is available as a Jupyter Notebook on my Github.
Import libraries and data
numpy for the logarithm function
pandas_datareader for the crypto data
matplotlib for plotting graphs

import numpy as np
from pandas_datareader import data as wb
import matplotlib.pyplot as plt
Set Number of Days in a Year
Crypto is traded 24/7 and is not limited to traditional market timings. If you want to calculate for stocks, change the constant below.
DAYS_IN_YEAR = 365.25
Let us Define the Functions
get_ticker_symbol(): gets the ticker symbol
get_start_date(): gets the start date. If none is specified, then MAX
get_simple_ror(data_frame): calculates simple ror
get_average_returns_daily(data_frame):calculates the average daily return
get_average_returns_annually(data_frame):calculates average returns annually
get_log_ror(data_frame):calculates the logarithmic rate of return
get_log_returns_daily(data_frame):calculates average daily log return
get_log_returns_annually(data_frame):calculates average log-returns annually

def get_ticker_symbol():
  return input("Enter Ticker Symbol: ")

def get_start_date():
  return input("Enter Start date from when you want to get data. Example: 2014-09-16 or enter for from the beginning of time: ")

# Get's data for specified Crypto or Security - Use Yahoo Finanace website as 
# reference.
def get_data(ticker):  
  data = wb.DataReader(ticker, data_source='yahoo', start=start_date)
  return data

def get_simple_ror(data_frame):
  data_frame['simple_return'] = (data_frame['Adj Close'] / data_frame['Adj Close'].shift(1)) - 1
  return data_frame['simple_return']

def get_average_returns_daily(data_frame):
  average_returns_daily = data_frame['simple_return'].mean()
  return average_returns_daily

def get_average_returns_annually(data_frame):
  average_returns_annually = data_frame['simple_return'].mean() * DAYS_IN_YEAR
  return average_returns_annually

def get_log_ror(data_frame):
  data_frame['log_return'] = np.log(data_frame['Adj Close'] / data_frame['Adj Close'].shift(1))
  return data_frame['log_return']

def get_log_returns_daily(data_frame):
  log_returns_daily = data_frame['log_return'].mean()
  return log_returns_daily

def get_log_returns_annually(data_frame):
  log_returns_annually = data_frame['log_return'].mean() * DAYS_IN_YEAR
  return log_returns_annually
Run the Program
# Get ticker symbol and start date. Press enter for max date.
# Run program - asks for user input
ticker = get_ticker_symbol()
start_date = get_start_date()
print()
# Get ticker symbol and start date. Press enter for max date.
# Run program - asks for user input
ticker = get_ticker_symbol()
start_date = get_start_date()
print()
# Analyze the dataset
print(symbol_dataframe.describe())
# Prints simple ROR
print(get_simple_ror(symbol_dataframe))
# Plot simple return
sror = get_simple_ror(symbol_dataframe)
sror.plot(figsize=(8,5))
# Print's simpl Avg returns daily
average_returns_daily = get_average_returns_daily(symbol_dataframe)
average_returns_daily
print("The average daily simple rate of return for " + ticker + " is " 
      + str(round(average_returns_daily, 5) * 100) + ' %')
# Print simple Avg returns annually
average_returns_annually = get_average_returns_annually(symbol_dataframe)
average_returns_annually
print("The average annual simple rate of return for " + ticker + " is " 
      + str(round(average_returns_annually, 5) * 100) + ' %')
# Print Log ROR
print(get_log_ror(symbol_dataframe))
# Plot log return
lror = get_log_ror(symbol_dataframe)
lror.plot(figsize=(8,5))
# Print daily log return
average_log_returns_daily = get_log_returns_daily(symbol_dataframe)
average_log_returns_daily
print("The average daily logarithmic rate of return for " + ticker + " is " 
      + str(round(average_log_returns_daily, 5) * 100) + ' %')
# Print annual log return
average_log_returns_annually = get_log_returns_annually(symbol_dataframe)
average_log_returns_annually
print("The average annual logarithmic rate of return for " + ticker + " is " 
      + str(round(average_log_returns_annually, 5) * 100) + ' %')
The source code is available as a Jupyter Notebook on my Github.
Here is the output
You can see the dip in March 2020 on the chart below due to COVID-19
Based on the output, the daily simple return is .75% and 274.98% annually. Based on the plot, the returns have mostly been positive. Next, we will plot the logarithmic rate of returns.
According to Chandler Fang, If one is modeling the stock[crypto] market, it is common to assume that returns are normally distributed. In this context, log returns are far superior to arithmetic returns since the sum of repeated samples from a normal distribution is normally distributed. However, the product of repeated samples from a normal distribution is not normally distributed.
However, that's not to say arithmetic returns aren't without their benefits. Arithmetic returns aggregate well across portfolios. The arithmetic return for a portfolio is simply equal to the weighted average of each constituent's arithmetic return.
But, more importantly, for forensic settings, arithmetic returns are widely understood by the public. Confidently explaining complex topics to laymen separates good and great expert witnesses. For that reason alone, we normally rely on arithmetic growth rates when they do not produce an error.
According to the log-returns DOGE coin looks like a very profitable option, all things being equal. Feel free to download and play around with the code. This is all for your knowledge so feel free to share!
