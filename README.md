# Portfolio Optimization Using Pyomo
In this project, I am trying to create an optimized investment plan for investors interested in the stock market - and I am going to use required disclosures from Members of Congress to help build a portfolio.

### Data
Data set is the raw stock data of one of the Members of Congress. More details about this data set are in the links below:

https://senatestockwatcher.com/summary_by_senator/James%20M%20Inhofe

_As a part of EDA & pre-processing, using the Yahoo Finance API to pull the historical stock price data from January 1, 2015 to March 1, 2020._

### Decision Variables
We will consider the top 10 stocks from the Senator's portfolio using a specific methodology. The allocated proportion of each of these 10 stocks in the budget (from the model built on nonlinear solver) are our decision variables. 

### Objective
To create a portfolio that balances the conflicting variables of risk and profit appropriately given differing criteria. 
Given a set of assets and a budget, the goal is to select the amount of money to allocate to each asset such that:

a. The expected income of the selected portfolio is equal to some predefined value; and
  
b. The goal is to minimize the risk, which is given by the covariance (risk) of the portfolio.
  
We are trying to allocate money into stocks in order to maximize the return while accounting for a risk tolerance - but we can’t optimize two conflicting quantities (profit and risk) at once. Instead, we will take a more piecewise approach - where for each given risk tolerance ceiling (the max amount of risk we are willing to take on), we will try to maximize profit for that given risk level. So we will calculate one optimal mix of allocation of stocks that maximizes profit for each risk level. 

Low risk levels will have well-balanced and diversified portfolios but we will only make a little bit of money. High risk levels will have very skewed/narrow portfolio mixes (like only buying Amazon or Google in your portfolio!) but this can be highly volatile. The goal is to show the range of outcomes of profit we could achieve for all risk levels (known as the efficient frontier).

### Constraints 
The solutions should satisfy the following constraints:

First, the sum of allocated proportions of 10 stocks should sum up to 100% or 1 which is the total or maximum percentage. Hence, while declaring the variables, the bounds for the same must be between 0 and 1. 
Second, assuming a minimum return such that the maximized portfolio return from the objective function must be greater than or at least the minimum return assumed (Ex: 0.005% per day) 
