# Stock Risk Management Dashboard

The Stock Risk Management Dashboard is an intuitive tool designed to compare and analyze the performance of 10 stocks across various sectors. By offering sector-wise insights and visual comparisons, it helps users make data-driven decisions to optimize their investment portfolios and mitigate financial risks effectively.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Screenshots](#screenshots)
- [Technologies Used](#technologies-used)
- [Live Link](#live-link)

## Overview
The Stock Risk Management Dashboard is an interactive platform designed to provide a comprehensive analysis of 10 stocks from various sectors. The dashboard empowers users to make informed investment decisions by visualizing data trends, comparing sector-wise performance, and identifying potential risks.
This dashboard has various metrics to judge the performance of the stock like moving averages, time value of money, etc.
With features like historical performance tracking, volume trades, and comparative analysis, the dashboard provides a holistic view of stock behavior. It also allows users to identify trends, assess risk levels, and align investment choices with their financial goals.

Whether you're a seasoned investor or new to the stock market, this dashboard serves as a reliable resource for gaining actionable insights and making data-driven decisions with confidence.


## Features
- 📊 **Risk Analysis**: Identify potential risks through observed patterns such as bullish, bearish, or neutral trends.
- 📈 **Data Visualization**: Generate insightful charts and graphs to track stock performance and sector trends.
- 🔍 Stock Insights: Provide detailed and actionable insights about stock performance to support informed decision-making.

## Screenshots


Lets take an example of stock **Apple (APPL)**:


![image](https://github.com/user-attachments/assets/e79b44f6-3482-4e9e-b515-77cd324f8761)


The Dashboard provides a detailed overview of Apple's stock trends from **January 2, 2014, to December 31, 2024**. The dashboard includes visual representations of the stock's closing prices and moving averages (10-day, 20-day, and 50-day), offering a clear view of its growth trajectory over time. The line chart highlights the consistent upward trend in the stock's value, indicating **bullish momentum** in recent years.

A pie chart illustrates the annual volume distribution, offering insights into the trading activity year by year, with noticeable peaks that reflect higher investor interest or market events. Key stock information, such as the **starting closing value ($17.23)** and **ending closing value ($250.42)**, is prominently displayed, emphasizing the substantial growth over the analyzed period.

The dashboard also evaluates market direction (bullish, bearish, or neutral) using trend signals, which classify Apple's current state as "bullish." Users can interact with the date range slider to customize the analysis period and assess performance for specific durations. Additionally, the comparative view allows investors to analyze Apple's performance alongside other stocks, facilitating sector-wide or cross-stock comparisons. 

**Note**: Data is imported via python scripting in power bi which can be refreshed again which will reflect the latest stock values.Each of the stock values is in **USD**.

---

**All other stocks:**

**AMD (AMD)**:

![image](https://github.com/user-attachments/assets/4bc4467c-002d-4541-b917-2b3750656672)


**Amazon (AMZN)**:

![image](https://github.com/user-attachments/assets/39828f79-9956-41b2-91e2-3894cbe6b1c1)


**Google (GOOGL)**:

![image](https://github.com/user-attachments/assets/58a36449-d026-4736-8385-e7e0987a8643)


**Goldman Sachs (GS)**:

![image](https://github.com/user-attachments/assets/49f17b25-99e0-442c-ba93-c8f86ad10898)


**Intel (INTC)**:

![image](https://github.com/user-attachments/assets/4da675b5-34b7-4edc-ae9a-deecd5dc2ca4)


**Meta (META)**:

![image](https://github.com/user-attachments/assets/3fddb279-adf2-4af6-9649-22b001cb8791)

**Microsoft (MSFT)**:

![image](https://github.com/user-attachments/assets/fc6d8dad-4193-4272-b17e-5ead9bbc5125)


**Nvidia (NVDA)**:

![image](https://github.com/user-attachments/assets/ea902334-7a7f-4fa5-b552-b0fce0667bd1)


**Tesla (TSLA)**:

![image](https://github.com/user-attachments/assets/f0ad3ef7-db49-4325-9c0c-b3ddd847f169)

---

### Principle of Time Value of Money (TVM)

The **Time Value of Money (TVM)** is a fundamental financial principle that states that money available today is worth more than the same amount in the future due to its earning potential. This is because money today can be invested to generate returns, leading to a greater value in the future.


![image](https://github.com/user-attachments/assets/7547d9bd-7ec7-414c-919c-41eed8edd82e)


### Key Formulae in TVM

#### 1. **Future Value (FV)**
The value of an investment at a specific time in the future, considering the interest rate and the compounding effect.


![image](https://github.com/user-attachments/assets/070e8f7f-d944-412e-84f6-f5acd66c9268)


- **FV**: Future Value  
- **PV**: Present Value  
- **r**: Annual interest rate (in decimal form)  
- **n**: Number of periods (years, months, etc.)  

#### 2. **Present Value (PV)**
The current worth of a future sum of money or cash flows given a specified rate of return.

![image](https://github.com/user-attachments/assets/942b0b9d-8ac2-4ef3-91ab-8169b2adc222)


- **PV**: Present Value  
- **FV**: Future Value  
- **r**: Annual interest rate (in decimal form)  
- **n**: Number of periods  

---

### Example: Future Value Calculation

#### Scenario:  
You invest $1,000 today in a savings account that offers a 5% annual interest rate compounded yearly. You want to calculate its value after 5 years.

#### Solution:  
Using the **Future Value (FV)** formula:

![image](https://github.com/user-attachments/assets/498b3b06-00f9-404f-bbb5-e808ca894fac)


#### Result:
After 5 years, your investment will grow to **$1,276.28**.

Similarly, the **forecasted future value** has been calculated for every stock each data and plotted in the graph.

---

## Technologies Used

Python scripting as been used to get the data from **Yahoo finance**

Step 1:
Install Required Python Packages

```Python
pip install yfinance pandas
```

Step 2:

1.Write Python Script Inside Power BI

2.Open Power BI Desktop.

3.Go to Home → Get Data → More → Python Script.

4.Paste this Python script:

```Python
import pandas as pd
import yfinance as yf
from datetime import datetime

# List of Stocks
tickers = ["AAPL", "GOOGL", "MSFT", "AMZN", "META", "TSLA", "NVDA", "AMD", "GS"] #Add stocks to be observed

# Create Dictionary to Store Tables
stock_data = {}

for ticker in tickers:
    data = yf.download(ticker, start="2014-01-01", end=datetime.now().strftime("%Y-%m-%d"))
    data['MA_10'] = data['Close'].rolling(window=10).mean()
    data['MA_20'] = data['Close'].rolling(window=20).mean()
    data['MA_50'] = data['Close'].rolling(window=50).mean()
    data.reset_index(inplace=True)
    
    # Store DataFrame in Dictionary
    stock_data[ticker] = data[['Date', 'Open', 'High', 'Low', 'Close', 'Volume', 'MA_10', 'MA_20', 'MA_50']]
```
Step 3:

As per your requirement conslidate the data and more columns like starting price, end price, yearly return and much more using DAX formula. 

Step 4:

Make visualisations and done ! 

---

## Live Link 

Here are the live link of the Power Bi dashboard:

[Power Bi](https://app.powerbi.com/links/gm-9hK5Nr5?ctid=f5b4681f-f82a-4df9-b326-e69f9f8d0c13&pbi_source=linkShare&bookmarkGuid=2ad6aaf3-7a4d-4761-84e9-1d048ea05b62)













