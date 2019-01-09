# Stocks-Risk-Analysis
Perform the financial risk analysis on a stocks portfolio, through Monte Carlo Simulation and Multiple Linear Regression.

## Project overview
### Purpose
The goal of this demo is to build a predicion model able to indicate the VaR (Value at Risk) for a given stock portfolio: in other words, an indicator of how much the global value of our stocks will increase/decrease in a given time interval. To be more precise, the VaR indicates (with a given confidence level) the expected lower bound of the losses we can expect.

Given the stock values and the market factors dataset, the first step is to analyze them and pre-process the data (for example: some temporal stock values may be missing). Then, the Linear Regression model is built and the Monte Carlo Simulation run in parallel, over the cluster.

## Technical details
### Apache Spark
The framework is used to run (in parallel) 10000 times the MCS. In our case, the parallelism factor was 12.

### Data Science Python libraries
- Pandas and Numpy: data processing and analysis
- Scipy and StatsModels: for the statistics
- Matplotlib and Seaborn: data visualization

### The mathematical model
The risk analysis starting point is a Multiple Linear Regression model, which tries to predict the two-weeks stock returns starting from 4 market factors. Non-linear dependencies are taken into account, thanks to the featurization (we have considered, for each feature, also its square and square root values).

The market factors we have (for the period: 23/01/2009 - 22/01/2014) are:
- GSPC value
- IXIC value
- The return of crude oil
- The return of treasury bonds

After the model is built, the MCS (Monte Carlo Simulation) is run 10.000 times. In this way, we can exploit the output obtained probability distribution in order to determine the VaR 5% (Value at Risk: the 5th percentile of the losses).
