# ESG_Trading_Strategy

Feed with ESG dataset on strategies


Strategy Overview:

1. Define the Stock Universe
We start by specifying that we will constrain our search for pairs to a large and liquid single stock universe.

2. Given the pricing data, fundamental data, and ESG data, we will first classify stocks into clusters. Within clusters, we then look for strong mean-reverting pair relationships.
3. 
The first hypothesis above is that “Stocks that share loadings to common factors in the past should be related in the future”. Common factors are things like sector/industry membership and widely known ranking schemes like momentum and value. We could specify the common factors a priori to well known factors, or alternatively, we could let the data speak for itself. We take the latter approach. We use PCA to reduce the dimensionality of the returns data and extract the historical latent common factor loadings for each stock. For a nice visual introduction to what PCA is doing, take a look here.
We take these features, add in the fundamental and ESG features, and then use the DBSCAN unsupervised clustering algorithm which is available in scikit-learn. DBSCAN has advantages over KMeans in this use case, specifically:
DBSCAN does not cluster all stocks; it leaves out stocks which do not neatly fit into a cluster.

As a result, you do not need to specify the number of clusters.

The clustering algorithm will give us sensible candidate pairs. We will need to do some validation in the next step.

3. We take a Bayesian approach to pairs trading using probabilistic programming, which is a form of Bayesian machine learning. Unlike simpler frequentist cointegration tests, our Bayesian approach allows us to monitor the relationship between a pair of equities over time, which allows us to follow pairs whose cointegration parameters change steadily or abruptly. When combined with a simple mean-reversion trading algorithm, we demonstrate this to be a viable theoretical trading strategy, ready for further evaluation and risk management

4. Knowing that two stocks may or may not be cointegrated does not explicitly define a trading strategy. For that we present the following simple mean-reversion style trading algorithm, which capitalizes on the assumed mean-reverting behavior of a cointegrated portfolio of stocks. We trade whenever our portfolio is moving back toward its mean value. When the algorithm is not trading, we dynamically update 𝛽 and its other parameters, to adapt to potentially changing cointegration conditions. Once a trade begins, we are forced to trade the two stocks at a fixed rate, and so our 𝛽 becomes locked for the duration of the trade. The algorithm’s exact implementation is as follows:

Define a “signal”, which should mean-revert to zero if 𝛽 remains relatively stationary.

Define a “smoothed signal”, a 15-day moving average of the “signal”.

If we are not trading…
Update 𝛽 so that it does not remain fixed while we aren’t trading.

If the smoothed signal is above zero and moving downward, short our portfolio.

If the smoothed signal is below zero and moving upward, go long on our portfolio.

If we are trading long…

If the smoothed signal goes below its start value, close the trade; we may be diverging from the mean.

If the smoothed signal rises through the zero line, we’ve reached the mean. Close the trade.

If we are trading short…

If the smoothed signal goes above its start value, close the trade; we may be diverging from the mean.

If the smoothed signal falls through the zero line, we’ve reached the mean. Close the trade.


