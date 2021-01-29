The goal of this challenge is to predict the volume (total value of stock exchanged) 
available for auction, for 900 stocks over about 350 days. 


What is an auction ? 


"Accodring to AMF report octobre 2019, the increasing concentration of share trading volumes at the end of the day is a phenomenon that can be witnessed to varying degrees on all the main markets worldwide. 
However, France is one of the markets on where this trend has reached the highest levels, with close to 41% of CAC 40 volumes traded at the closing auction on Euronext Paris in June 2019. 
This rate is well above the 12%-14% level seen in the United States.

Why this increase ? 
- The rapid growth in passive management, for which unit creation and cancellation generally takes place at the end-of-day liquidation value and for which a precise replication entails trading at the closing price;
- The obligation of “best execution” and especially reporting obligations of the “Trade & Cost Analysis” type to which fund managers have been subject since the application of MiFID II. By trading at the closing auction, this type of reporting becomes superfluous;
- A move to avoid HFTs arbitrageurs, who rarely get involved in the closing auction phase;
- Lastly, the role of execution algorithms, which have amplified the above factors, since liquidity attracts liquidity.

While volumes and prices converge rapidly towards their final level during the first half of the order accumulation phase (90% of the volumes traded are already present in the order book with an average price differential of 0.30%), final convergence takes place in the last 15 seconds of the auction.


this change in market structure is accompanied by the emergence of certain risks, in particular an increased exposure to operational incidents, which could occur during this very brief phase, and lower levels of liquidity in the rest of the session"

Cf ressource & note documentaire



   
Input data : 
The prediction of the auction volume for a given stock on a given day can be made based on the following 126 input columns:

- pid: a Product ID, that represents a stock.
- day: day of the data sample, as an integer. The ordering is chronological, with day 0 coming before day 1, etc.
- abs_retn (n from 0 to 60): absolute values of stock returns (relative price change) between the last known price (typically the price at the beginning of period n) and the end of period n (as a percentage), where the periods cover a good part of the trading day, don't overlap, and have the same duration. Return n=0 comes before return n=1, etc.
- rel_voln: like abs_retn, but represents the traded stock volume as a fraction of the volume traded during the period covered (thus, they sum to 1, over a day). The periods are the same as for the returns.
- LS and NLV: two quantities associated with the trades of the day for the stock in question. Their nature is kept undisclosed for this challenge.
  


Abs_return : measurement of the volatility of the share during one day over 61 time intervals
Rel_voln : fraction of the volume exchanged during the day at different times of the day. Total volume in dollar




Output data : 


The output data contains, for a given stock and a given day, the natural logarithm of the auction volume (= total value of traded stocks), as a fraction of the total volume in the 61 given periods. 
Thus, if the auction volume represents 10 % of the volume traded over all the periods of a day, the target is log 0.10 = -2.30…

Nb of days * 900 = around 320 000 lines

Training & Test data : 
  
The 900 stocks found in the training and test data are the same: it is therefore in principle possible to devise predictions that are customized for each stock.

The training data contains information on about 800 different days, while the test data requires auction volume predictions for about 350 days.

Furthermore, the test inputs correspond to days that come after those of the training data. A challenge is that auction volumes can evolve over time (for instance by becoming relatively larger and larger over time), but we only see what the past (training) auction volumes looks like.


=

Benchmark : 
  
The benchmark is built by first inputing all the missing values by zero, and then performing a linear fit on all the columns, stock Product ID (pid) excepted.

The difference between the predictions of this linear model and the known (training) targets is then predicted by gradient tree boosting (with LightGBM) on all the columns (hence including the stock IDs). 
The boosted trees are trained with early stopping, and a cross-validation that measures future predictions after a training on (mostly) past data (with sklearn.model_selection.TimeSeriesSplit). 
All the other settings are the default ones.