# The Role of Cryptocurrency in Optimizing a Mixed-Asset Portfolio

This section is just for financial reporting and analyzing only. Back-end code in Python could be found here.

## Table of Contents 
1. Executive Summary 
2. Data Import
3. Financial Analysis
4. Portfolio Optimization
5. Conclusions

## 1. Executive Summary
On the last trading day of 2022 (December 30th), the Wall Street Journal claimed the year of 2022 as **"[one of the worst years for markets in recent history](https://www.wsj.com/articles/global-stocks-markets-dow-update-12-30-2022-11672403899)"**. Not only bonds but also risky assets like stocks and cryptocurrencies faced extreme crashes in price. Especially, the most popular cryptocurrency - **Bitcoin** - finished 2022 with a price of only around 17,000 USD - a significant drop from its all-time high of over 65,000 USD in November 2021. Yet, before the "Crypto Winter" came, Bitcoin and other cryptocurrencies had had a meteoric rise during the pandemic before reaching their all-time high in late 2021. This leads to the fact that even currently suffering from a great discount, a huge number of long-term cryptocurrency holders still outperformed the market. Given this information, the question here is **whether or not an allocation to Bitcoin would improve the overall performance of a traditional portfolio which includes a set of various securities**.  

In order to answer this question, this report will collect and analyze the performances of Bitcoin along with seven different securities from the start of 2016 to the end of 2022. By doing so, this report will address several questions, including:
* How does the performance of a cryptocurrency like Bitcoin compare to other securities in terms of risks and returns?
* Does the allocation of Bitcoin help improve the overall performance of the portfolio? 
* Could Bitcoin help in hedging high inflation?
* Given the high risk of Bitcoin, is it possible to lower risk while improving the overall returns through portfolio diversification?

While the first three questions will be answered with basic financial analyses, the fourth will be addressed by applying the Modern Portfolio Theory (MPT) or Mean-Variance Analysis, a mathematical method for selecting a variety of investments in order to optimize the overall returns in a period of time for a given level of risk. 

Conclusions could be found at the end of each sections, as well as at the end of the report. 

**Caution:** This report is built on historical data collected in a short period of time (2016-2022). It might be considered an approach to address the above questions but absolutely not the only approach. Thus, it would not be extrapolated into the future, and the future trend might be significantly different. 

## 2. Data Import 

### a. Stocks and Bitcoin Data
Stocks and Bitcoin Data are directly downloaded from **[Yahoo Finance](https://finance.yahoo.com/)** through Python module **yfinance**.

Data collected include: 
* **date**: date recorded 
* **open**: opening price for a given day
* **high**: highest price recorded for a given day
* **low**: lowest price recorded for a given day
* **close**: closing price for a given day
* **volume**: number of shares traded for a given day
* **adjusted**: adjusted closing price after accounting for any corporate actions of the company for a given day.

The data collected consists of daily recorded data for AAPL, BAC, F, HAL, KO, OXY, and QCOM (no missing data for every trading day from Jan 04, 2016 to December 30, 2022), along with Bitcoin (BTC-USD) data (no missing data for every day (include weekend) from Jan 01, 2016 to December 31, 2022).

### b. Inflation Data
Inflation data (represented by the monthly **Consumer Price Index** or **CPI**) is downloaded from the **United States Bureau of Labor Statistics** through Python module **bls**. 

**Consumer Price Index** as of December 2022: 
| Year | Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **2016** | 236.916 | 237.111 | 238.132 | 239.261 | 240.229 | 241.018 | 240.628 | 240.849 | 241.428 | 241.729 | 241.353 | 241.432 |
| **2017** | 242.839 | 243.603 | 243.801 | 244.524 | 244.733 | 244.955 | 244.786 | 245.519 | 246.819 | 246.663 | 246.669 | 246.524 |
| **2018** | 247.867 | 248.991 | 249.554 | 250.546 | 251.588 | 251.989 | 252.006 | 252.146 | 252.439 | 252.885| 252.038 | 251.233 |
| **2019** | 251.712 | 252.776 | 254.202 | 255.548 | 256.092 | 256.143 | 256.571 | 256.558 | 256.759 | 257.346 | 257.208 | 256.974 |
| **2020** | 257.971 | 258.678 | 258.115 | 256.389 | 256.394 | 257.797 | 259.101 | 259.918 | 260.280 | 260.388 | 260.229 | 260.474 |
| **2021** | 261.582 | 263.014 | 264.877 | 267.054 | 269.195 | 271.696 | 273.003 | 273.567 | 274.310 | 276.589 | 277.948 | 278.802 |
| **2022** | 281.148 | 283.716 | 287.504 | 289.109 | 292.296 | 296.311 | 296.276 | 296.171 | 296.808 | 298.012 | 297.711 | NA |

## 3. Financial Analysis

### a. Assets' Historical Price and Volume

![Price Chart](https://user-images.githubusercontent.com/114312864/212120296-f9ffea7e-107e-405b-95ae-32fe859134bf.jpg)

![Volume Chart](https://user-images.githubusercontent.com/114312864/212121237-3a7d852a-026d-414d-8617-e15f9c929fa0.jpg)

### b. Cumulative Return
![Cumulative Return](https://user-images.githubusercontent.com/114312864/212122195-d9c950fb-c57e-456d-9ab2-3a01ab22cf29.jpg)

### c. Assets versus Inflation
![Asset vs CPI](https://user-images.githubusercontent.com/114312864/212123343-5c960fa5-6fd3-4312-87d1-fb190eef1202.jpg)

### d. Assets Risk based on Daily Returns
![Risk based on Daily Returns](https://user-images.githubusercontent.com/114312864/212123835-79b17034-a4e7-4edd-85cd-cc0e875832be.jpg)

### e. Assets' Sharpe Ratio
![Sharpe Ratio](https://user-images.githubusercontent.com/114312864/212124345-b70d9495-ed40-4da6-810b-760cb5d6c86e.jpg)

## 4. Portfolio Optimization
