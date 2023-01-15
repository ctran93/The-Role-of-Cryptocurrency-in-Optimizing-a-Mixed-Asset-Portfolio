# The Role of Cryptocurrency in Optimizing a Mixed-Asset Portfolio

This project is built and developed on my previous one [Modern Portfolio Optimization](https://github.com/ctran93/Modern-Portfolio-Optimization-R).

This section is just for financial reporting and analyzing only. Back-end code in Python could be found [here](https://github.com/ctran93/The-Role-of-Cryptocurrency-in-Optimizing-a-Mixed-Asset-Portfolio/blob/main/The%20Role%20of%20Cryptocurrency%20in%20Optimizing%20a%20Mixed-Asset%20Portfolio.ipynb).

## Table of Contents 
[I Executive Summary](#i-executive-summary) 

[II Data Import](#ii-data-import)

* [1 Stocks and Bitcoin Data](#1-stocks-and-bitcoin-data)
* [2 Inflation Data](#2-inflation-data)

[III Financial Analysis](#iii-financial-analysis)
* [1 Statistical Data](#1-statistical-data)
         + [a Return](#a-return)
         + [b Risk (Standard Deviation)](#b-risk-(-standard-deviation-))

[IV Portfolio Optimization](#iv-portfolio-optimization)

[V Code Running Video](#v-code-running-video)

## I Executive Summary
On the last trading day of 2022 (December 30th), the Wall Street Journal claimed the year of 2022 as **"[one of the worst years for markets in recent history](https://www.wsj.com/articles/global-stocks-markets-dow-update-12-30-2022-11672403899)"**. Not only bonds but also risky assets like stocks and cryptocurrencies faced extreme crashes in price. Especially, the most popular cryptocurrency - **Bitcoin** - finished 2022 with a price of only around 17,000 USD - a significant drop from its all-time high of over 65,000 USD in November 2021. Yet, before the "Crypto Winter" came, Bitcoin and other cryptocurrencies had had a meteoric rise during the pandemic before reaching their all-time high in late 2021. This leads to the fact that even currently suffering from a great discount, a huge number of long-term cryptocurrency holders still outperformed the market. Given this information, the question here is **whether or not an allocation to Bitcoin would improve the overall performance of a traditional portfolio which includes a set of various securities**.  

In order to answer this question, this report will collect and analyze the performances of Bitcoin along with seven different securities from the start of 2016 to the end of 2022. By doing so, this report will address several questions, including:
* How does the performance of a cryptocurrency like Bitcoin compare to other securities in terms of risks and returns?
* Does the allocation of Bitcoin help improve the overall performance of the portfolio? 
* Could Bitcoin help in hedging high inflation?
* Given the high risk of Bitcoin, is it possible to lower risk while improving the overall returns through portfolio diversification?

While the first three questions will be answered with basic financial analyses, the fourth will be addressed by applying the Modern Portfolio Theory (MPT) or Mean-Variance Analysis, a mathematical method for selecting a variety of investments in order to optimize the overall returns in a period of time for a given level of risk. 

Conclusions could be found at the end of each sections, as well as at the end of the report. 

**Caution:** This report is built on historical data collected in a short period of time (2016-2022). It might be considered an approach to address the above questions but absolutely not the only approach. Thus, it would not be extrapolated into the future, and the future trend might be significantly different. 

## II Data Import 

### 1 Stocks and Bitcoin Data
Stocks and Bitcoin Data are directly downloaded from **[Yahoo Finance](https://finance.yahoo.com/)** through Python module **yfinance**.

Data collected include: 
* **date**: date recorded 
* **open**: opening price for a given day
* **high**: highest price recorded for a given day
* **low**: lowest price recorded for a given day
* **close**: closing price for a given day
* **volume**: number of shares traded for a given day
* **adjusted**: adjusted closing price after accounting for any corporate actions of the company for a given day.

The data collected consists of daily recorded data for AAPL, F, HAL, KO, OXY, QCOM, and TSLA (no missing data for every trading day from Jan 04, 2016 to December 30, 2022), along with Bitcoin (BTC-USD) data (no missing data for every day (include weekend) from Jan 01, 2016 to December 31, 2022).

### 2 Inflation Data
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
| **2022** | 281.148 | 283.716 | 287.504 | 289.109 | 292.296 | 296.311 | 296.276 | 296.171 | 296.808 | 298.012 | 297.711 | 296.797 |

## III Financial Analysis
### 1 Statistical Data
#### a Return 
* **Expected Daily Return** 

| Ticker | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **Expected Daily Return** | 0.000787 | 0.002188 | 0.000241 | 0.000448 |  0.000298 | 0.000500 | 0.000589 | 0.001300 |

* **Annualized Return** 

In order to find the annualied return, we multyply the expected daily return of each individual asset with 252 (the expected number of trading days per year)

| Ticker | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **Annualized Return** | 0.198249 | 0.551352 | 0.060746 | 0.112852 |  0.075146 | 0.125939 | 0.148326 | 0.327684 |

#### b Risk (Standard Deviation)
* **Daily Return Standard Deviation** 

| Ticker | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **Daily Return Standard Deviation** | 0.015906 | 0.038849 | 0.019636 | 0.025975 |  0.010109 | 0.028600 | 0.019930 | 0.030769 |

* **Annualized Standard Deviation** 

Similar to return, we need to annualized the Standard Deviation of each individual assets. Yet, this time, we multiply these statistics with square root of 252 instead to find the annualized standard deviations. 

| Ticker | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **Annualized Standard Deviation** | 0.252504 | 0.616708 | 0.311717 | 0.412338 |  0.160471 | 0.454008 | 0.316386 | 0.488449 |

#### Finding 1: 

According to the tables above, **Bitcoin** has the **highest expected annual return** of **55.1%**, followed by **Tesla Inc. stock (TSLA)** which has an expected capital gain of **32.8%** per year. Yet, these two assets also possess the **highest risk** with standard deviations of **61.7%** and **48.8%** per year respectively.

On the other hand, while having the **lowest rate of risk** with an annualized standard deviation of **16%**, **Coca-Cola Co. stock (KO)** only promises a rate of **7.5%** per year. **Aaple Inc. stock (AAPL)** seems to be a great option for the portfolio as the annual return rate is **19.8%** with a not-too-high annualized standard deviation of **25.2%**.

No comment is made at this point on other assets (F, HAL, OXY, and QCOM) as they have not given any significant statistical data on both return and risk. 

#### c Correlation

![Correlation Heatmap](https://user-images.githubusercontent.com/114312864/212310699-25df85db-8d5e-489c-bc6d-639a72446275.jpg)

#### Finding 2: 

The heatmap of Correlation among Assets suggests that Bitcoin has negligible correlations to other assets in the portfolio. All of the correlation related to Bitcoin are less than 0.2 with the lowest ones are 0.076 and 0.086 belonging to Bitcoin's correlations to Coca-Cola Co. stock (KO) and Occidental Petroleum stock (OXY), respectively.  A correlation of approximately 0 means there is no clear relationship between the two assets; and it could be concluded that the two assets' movements are independent. 

On the other hand, a positive high correlation (approaching to 1), such as the correlation of 0.741 between Halliburton Co. stock (HAL) and Occidental Petroleum stock (OXY), suggests that the two assets are likely to move in similar directions. They will increase or decrease together.

### 2 Historical Price and Volume
#### a. Price Chart
![Price Chart](https://user-images.githubusercontent.com/114312864/212313974-13fdc881-98b5-4296-9924-241b1d8e0da0.jpg)

#### b Volume Chart
![Volume Chart](https://user-images.githubusercontent.com/114312864/212314245-76726e46-2065-4752-ae7c-3be1e75a19f0.jpg)

### 3 Culmulative Return
#### a Cumulative Return Chart 
![Cumulative Return](https://user-images.githubusercontent.com/114312864/212315958-f0d12102-866e-4866-92c0-c7610851b852.jpg)

#### b Value at the end of 2022 (start with $100 on January 4, 2016)
| Date | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **2022-12-30** | 538.871467 | 3833.509772 | 113.45628 | 129.374193 |  187.704681 | 118.901178 | 271.605507 | 827.044447 |

#### Finding 3: 
The Price Chart illustrates the performances of each individual assets over the observation period. All of eight assets ended 2022 with positive capital gains. Yet Bitcoin still outperformed the market.  According to the Cumulative Return Chart and Table, an investment of $100 in Bitcoin at the beginning of 2016 could result in more than $3800 at the end of 2022, corresponding to 3700% in return after 7 years. Apple Inc. and Tesla Inc. stocks also brought significant returns of 400% and 700%, respectively. 

According to the Price and Volume Charts, the outstanding increase in the price of Bitcoin might correspond with the rise of Bitcoin's volume over the observation period. While other assets' volume have been relatively stable throughout the period, Bitcoin observed a dramatic boom in popularity during 2017. The price of Bitcoin also had rised sharply since 2017. After reaching it all time high in 2021, Bitcoin dropped significantly in terms of both price and volume. 

### 4 Correlation to Inflation
#### a Correlation to Inflation Table
|  | AAPL | BTC-USD | F | HAL | KO | OXY | QCOM | TSLA |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| **CPI** | -0.007124 | -0.150121 | 0.035459 | 0.059927 | 0.057429 |  0.159703 | -0.079198 | -0.020098 |

#### a Correlation to Inflation Heatmap
![Asset vs CPI](https://user-images.githubusercontent.com/114312864/212319911-7cc033d9-0ecf-4f7a-bc95-4216ec23a6fd.jpg)

#### Finding 4:
Although having diverse correlations to Inflation (represented by the Consumer Price Index, or CPI), observed assets all have negligible correlation to Inflation with the size of correlation from -0.3 to 0.3. 

With correlations from -0.1 to 0.1, Apple Inc. (AAPL), Ford Motor Company (F), Halliburton Co. (HAL), Coca-Cola (KO), Qualcomm (QCOM), and Tesla Inc. (TSLA) stocks might be great investments during high inflation period as numbers suggest that there might be no consistent relationship between price changes of these assets and inflation since 2016. 

On the other hand, Bitcoin might not be a great investment during high inflation time but deflation as the negative correlation of -0.15 suggests that Bitcoin price tends to decrease during increasing inflation period. In contrast, a positive correlation of 0.16 between Occidental Petroleum stock (OXY) and CPI indicates that this stock and inflation tend to move in the same direction. This conclusion, in fact, is reasonable as both energy companies like Occidental Petroleum and inflation are significantly positively influenced by energy price. 

### 4 Individual Assets' Risk
#### a Assets' Risk based on Daily Returns
![Risk based on Daily Returns](https://user-images.githubusercontent.com/114312864/212326925-92d5777c-fbe5-4a14-918b-6a02b1c46a76.jpg)

#### Finding 5: 
The above box plot shows that Bitcoin had the largest interquartile range with more positive outliners, corresponding with the highest daily expected return of this asset mentioned previously. AAPL and KO, according to this box plot, are considered safe investments as having the smallest spreads. It is also noticeable that even having a small interquartile range, OXY seems to be a risky investment with the largest range. OXY return could decrease by more than 50%, while positively, it could also reach a positive return of more than 30% in just a day. 

#### b Assets' Risk based on Sharpe Ratio

Sharpe Ratio is a measure to compare the return of an investment with its risk. 
Sharpe Ratio is calculated by the following calculation:

**Sharpe Ratio = $\frac{R - R_f}{\sigma}$** in which 
* R: Return of Asset or Portfolio
* $R_f$: Risk-free rate
* $\sigma$: Standard Deviation of Asset or Portfolio

The higher the Sharpe Ratio, the more attractive the risk-adjusted return. 

In order to find the Sharpe Ratio of each individual asset, the Risk-free rate is set at 0. 

![Sharpe Ratio](https://user-images.githubusercontent.com/114312864/212330918-711d2d26-ac1f-4eee-9a22-a2e7fc126ad9.jpg)

#### Finding 6:
Given the highest Sharpe Ratios of 0.894, 0.785, and 0.67, Bitcoin, AAPL, and TSLA are considered attractive investments for the portfolio. These three assets seem to take significant allocation in the optimal portfolio. 

On the other hand, with the lowest Sharpe Ratio of 0.195, F might not a such an attractive asset to include in the overall portfolio.

## IV Portfolio Optimization 

### 1 Risk-free Rate 
For the sake of simplicity, the annual Risk-free rate is set at 0. However, for other considerations, the risk-free rate might be set differently, for example, equal to the One-year Treasury Bill Rate of the United States Government. 

### 2 Portfolio Optimization

#### a Monte Carlo Simulation 
The Monte Carlo simulation in this project will calculate the annualized expected return and standard deviation of portfolios with random weights. The number of trials in the simulation is set at 10,000. These trials, later, will be used to find the Efficient Frontier.  

#### b Efficient Frontier
The Efficient Frontier is all the scatter points, each representing a given portfolio's expected return and its corresponding minimum variance. Any portfolio located on the Efficient Frontier would have a higher expected return than any other portfolio having the same variance. Similarly, any portfolio located on the Efficient Frontier would have a lower risk (lower variance) than any other portfolio having the same expected return. Investors, thus, should only consider portfolios laying on the Efficient Frontier.

The Efficient Frontier is limited by the minimum and maximum expected returns. While the minimum expected return is determined by the lowest expected return of all securities, the maximum expected return is determined by the highest one. No portfolio has an expected return beyond this bound.

![Eff_Frt](https://user-images.githubusercontent.com/114312864/212340506-021fc1e9-5bef-4f7b-b361-07890b78950a.png)

#### c Optimal Portfolios 
The Optimal Portfolio is defined as the portfolio having the highest possible Sharpe Ratio. 

##### Optimal Portfolio Allocation and Statistics with Bitcoin

Weights: AAPL: 0.41041
         BTC-USD: 0.30714
         KO: 0.10849
         TSLA: 0.17396
Expected annual return: 31.6%
Annual volatility: 27.6%
Sharpe Ratio: 1.07
![With Bitcoin](https://user-images.githubusercontent.com/114312864/212344196-cec100fb-bcfd-42ec-9091-56d6c156266f.jpg)

##### Optimal Portfolio Allocation and Statistics without Bitcoin

Weights: AAPL: 0.58045
         KO: 0.18844
         TSLA: 0.23111
Expected annual return: 29.7%
Annual volatility: 28.1%
Sharpe Ratio: 0.99

![Without Bitcoin](https://user-images.githubusercontent.com/114312864/212346132-659e1b37-3dbe-40b1-8891-d3abb15cecfd.jpg)

#### Overal Conclusion:
With a higher annual expected return (31.6% compared to 29.7%) and lower standard deviation (27.6% compared to 28.1%), the inclusion of Bitcoin will improve the overall performance of the portfolio, despite the sharp decrease in the price of this asset in 2022. 

## V Code Running Video

https://user-images.githubusercontent.com/114312864/212356254-3ce37e70-a3bf-4db4-866b-e860a94b1fba.mp4
