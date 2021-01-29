Idées présentation : 
- l'évolution du volume dans le futur n'est pas forcement linéaire
=> Feature : Evolution du volume globale par jour

- Pour un jour donné (cf idée rapport amf, election), le marché peut se comporter de manière particulière qui peut avoir des csq sur le volume. 


- Pour les arbres boostés, mauvais pour les extrapolations sur des données futurs (dans un domaine particulier
=> On peut les combiner avec d'autres algo


Idees from AMF report (only for France): 

A voir si piste valable avec origine marché diversifié (data US, EU, France ?)

- In a given quarter, the auction share for end-of-quarter months (March, June, September and December) is about 4% to 6% higher than that observed for the other months (bc of derivative product)
=> Fature Need quarter feature encode / months

- The days on which quarterly derivatives expire are not only amongst the most active days, they are also the days on which the share of the closing auction reaches its highest level cf graph amf

=> Encoder ces jours spécifiques

- last trading day of the months of February, May, August and November are also among the most active days in terms of volumes traded (to a lesser extent than for quarterly expiries) and those with the largest share of the fixing
This comes from The MSCI indices rebalancing days

=> Encoder ces jours 


- In contrast, on days of high volatility and large volumes (e.g. start of February 2018 and around the first round of the French presidential elections), 
the share of the closing auction is generally lower than the average on the other days.


- Phenomenon affecting all EU markets

In particular, the Euro Stoxx 50 Index is the most frequently replicated index in Europe by passive management, whose impact is particularly important at the closing auction


=> Add the Euro Stoxx 50 Index inside stock value in training and test set

- For the US market

8% in 2017 this share is estimated between 12% and 14% of the daily volumes in 2019.
hand-in-hand with an increase in the share of the last half-hour of the session


- Origin 

- RAPID DEVELOPMENT OF PASSIVE MANAGEMENT in Europe notably the ETF which have to increase their volume at the end of the day (vs US)
=> If we have the days, we could add the share of passive funds in equity funds

- Best Exectution obligation : since the closing auction offers a single simple reference price.

- Avoiding HTF

- THE AMPLIFYING EFFECT OF EXECUTION ALGORITHMS
VWAP type, which adapt their execution volumes to that of the market in general

=> Newcolumn : Abs_var_price* Abs_vol


- Check TOP & TOV formation in doc. 


