# ESG_Trading_Strategy

Feed with ESG dataset on strategies and get momentum return and sharpe ratio


Strategy Overview:

a.Determine the number of stocks to be used in the investment strategy portfolio as 1/10th of the number of stocks in each sector in the customized benchmark on a particular rebalancing date. For e.g., If IT sector had 62 stocks in the customized benchmark on a particular rebalancing date, it would have 6 stocks in the strategy portfolio.

b. Relative Momentum: Calculate the ESG 1 year Momentum for each stock in the customized benchmark. Formula used: ESG_MOM_1Y = ESG_Score(t)/ ESG_Score(t-1) – 1 {Here ESG_Score is the MSCI published Industry Adjusted ESG Score}

c. Absolute Momentum: using the following formula: ESG_MOM_1Y = ESG_Score (t) - ESG_Score (t-1)

d. Remove the stocks that had infinite calculated 1 year ESG Momentum as such companies had only recently started disclosing their ESG metrics and this infinite momentum was not an accurate representation of improvement in their ESG practices.

e. Within each sector group, rank the stocks in the descending order of their ESG Momentum values.

f. For each sector, select the highest ranked stocks (number of stocks to be selected is determined using Step 2.a.). E.g.: 9 stocks selected in Information Technology sector on 31 Dec 17 will have the highest 1 yr ESG momentum in the IT sector on that particular day.
