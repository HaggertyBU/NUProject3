# Gamma exposure on market move(spx)

## **Project Overview**

### *Packages Installed*
'pip install x' where 'x' is the package listed below:
* 'python == 3.9.1'
* 'yfinance'
* 'cufflinks == 0.17.3'
* 'seaborn == 0.14'
* 'statsmodels == 0.13.2'
* 'treeinterpreter ==0.2.0'
* 'SVR == 0.5'
* 'regressor 1.0.7'

###  *Files Explorer*
* 'DATA': Directory contains all original csv files
* 'PLOTS':  Directory containing all images of plots created in Jupyter Notebook

### Option Basics

To explain the basis of our project, one must have a basic and general understanding of what options are, and how they operate. There are two types of options, call options and put options. If an investor or trader believes that an equity is going to go up, they would purchase a call option. If an investor or trader believes that an equity is going to go down, they would purchase a put option. If a call option is purchased, the investor or trader has the right – but not the obligation - to buy 100 shares of the underlying equity at an agreed upon price for a specific period of time. If they purchase a put option, the investor or trader has the right – but not the obligation - to sell 100 shares of the underlying equity at an agreed upon price for a specific period of time. The “agreed upon price” in the prior sentence is referred to as the “strike price” of the option. 

The above is best described in an example. Let’s say it is January, the beginning of the New Year, and an investor wants to put their previous year-end bonus to work. Over the holidays, they saw numerous ads on TV for a new Apple product and they believe that Apple will have a strong year financially. The investor could then decide that they would like to purchase a call option on Apple since they believe the stock will go up due to strong financial performance. The investor would then see what Apple is trading at. Let’s say Apple was trading at $150 per share and the investor believes Apple has the potential go up 20% this year to $180 per share. The investor could then buy $180 call options that expire at the end of the year. To purchase this option, the investor would pay a premium that covers the cost of the option. Let’s say that the premium cost of the option was $5 per share. The breakeven price for an option is equal to the strike price plus the premium paid for the option. For the example above, Apple stock would have to reach $185 per share for the option to breakeven. Since the investor purchased an option, they do not have forever to wait for the underlying to reach the strike price. If Apple’s stock does not reach $180 by the end of the year, the investor will lose their entire investment. However, if Apple stock were to outperform his expectations and trade up to $190 per share at the end of the year, the investor could “exercise” or execute his option and purchase the Apple stock at the previously agreed upon price at $180 per share. 

As we know, stock market prices are very dynamic and change very frequently. Options do the same. Option change according to their underlying asset. Below we will discuss a bit about how they change, through what is known as their “Greeks.”

### The Greeks

Option pricing is very complex, as it has multiple factors that go into it. Most options are priced through a method called the Black-Scholes Model. We aren’t going to cover that in this project, but instead we are going to cover what option traders refer to as “the Greeks.” The Greeks refer to an option’s “Delta”, “Gamma”, “Theta”, “Vega”, and “Rho.” Below we will cover each one and explain each of them individually. 

### Delta

Delta is the amount an option’s price would change based upon a $1 move in the stock.
Calls have a positive delta between 0 and 1, while puts have a negative delta between 0 and -1. Delta represents the number of relative shares you would own if you purchased an option at a specific delta. For example, if you buy a call option with a .50 delta that is essentially equivalent to buying 50 shares of stock, and vice versa with put options, -.50 delta is the same as shorting 50 shares of the underlying stock.
Let’s say a stock priced at $100 has a $110 call option with a delta of .30 and costs $2.00. If the underlying stock moves up to $101, the option should now be worth $2.30. Owning 100 shares of the stock would have realized a gain of $100. The .30 delta option realized approximately 30 shares worth of value, or $30. Delta can also act as an approximation of the probability an option will finish in-the-money. A .30 delta has roughly a 30% chance of expiring in-the-money, or a 70% chance of expiring out-of-the-money.
Delta is sensitive to time as well as how close it is to the money. Options that are further out in time, have a higher delta than options that have a shorter time to expiration. The chart below illustrates this. 
 
As we see in the chart above, options with a sooner expiration (1W) have a steeper slope, therefore less delta, than options that are further out in time (9M). 

Deltas are also impacted by the implied volatility of the underlying stock. As implied volatility goes up, the delta of the option increases (in absolute terms). That effect is illustrated in the chart below. 











In the graph above, options with an Implied Volatility of 10, have a lower delta than options that have an Implied Volatility of 50.

### Gamma

Gamma is closely related to delta. Gamma is the rate of change in delta for every $1 change in the underlying equity price. Gamma represents the acceleration at which an option's price increases or decreases. Think of gamma as the next dollar move. 
For example, if an option has a delta of .40 and a gamma of .20, the first dollar move in the underlying asset will see the price of the option change by $0.40 ($40). The subsequent dollar move of the stock will see the price of the option change another $0.40 ($40) plus an additional $0.20 ($20). Therefore, a $2 move in stock price will result in a total net change of $1.00 ($100) in the option’s price.
Gamma is higher for contracts closer to at-the-money and more sensitive to changes in the underlying asset price. The chart below illustrates Gamma compared to underlying price. 

 
 Gamma risk is the concern that price changes in the underlying asset will have an adverse impact on the option premium. Gamma risk increases as options approach expiration because a small move in the underlying security will significantly impact pricing due to the lack of time remaining on the contract. The chart below illustrates the relationship between Gamma and time to option expiration. 



 

For this project, we will mainly focus on Delta and Gamma, but it is important to understand the effects that the rest of the Greeks have on pricing. 

### Theta

Theta represents the effect time decay has on the value of an option. Options are a decaying asset. Options contracts lose value daily from the passage of time. The rate at which options contracts lose value increases exponentially as options approach expiration. Theta is the amount the price of the option will decrease each day. For example, a theta value of -.02 means the option will lose $0.02 ($2) per day.
Theta is always represented in negative terms because the portion of an option’s value related to time is always going down. Theta value is smaller further away from expiration and is not constant -- it accelerates more rapidly the closer it gets to expiration. Theta is an advantage for the option seller and a disadvantage for the option buyer.

### Vega 

Vega is the amount option prices change for every 1% change in implied volatility in the underlying security. Vega represents an unknown element because future volatility cannot be predicted. All other components of an option’s price can be determined objectively: spot price, strike price, and time to expiration. Vega has no impact on the intrinsic value of an option. It is not based on price movement in the stock, only changes in volatility. As volatility increases, an option’s price increases as market participants anticipate an above-average move may be possible before expiration. Vega decreases as it approaches expiration because there is less time for volatility to occur.

### Rho

Rho measures the sensitivity of an option’s price as it relates to changes in interest rates. Rho represents the expected change of a contract’s value for a 1% change in interest rates. Rho is not as important for short-term options traders because changes in interest rates are usually relatively small, and only adjusted once per quarter, if at all.
Longer-dated options are more significantly impacted by changes in interest rates due to their long expiration period. Investors hedging long-term positions with options may also consider rho, as changes in interest rates will affect the value of those positions.


### Model Inputs 

In this section we will discuss the main inputs in our Machine Learning model. 


### The Volatility Index (VIX)

The Volatility Index, commonly referred to as the VIX, is a forward-looking index that was created by the Chicago Board of Options (CBOE). The basis for the VIX is to measure the expected magnitude of the price movements for the S&P 500. The higher the price of the VIX, the higher the volatility expectations are for the S&P. The VIX is derived from a series of S&P 500 put options for the ensuing 30 days from the current day. The VIX is a gauge and is non-tradeable. 

### Gamma Exposure (GEX)

Gamma Exposure measures the second order price sensitivity of an option in regard to changes in the price of the underlying asset.  Gamma Exposure is important due to the effect it has on underlying equities. When an option is bought, the entity who sells the option (market maker/ dealer), becomes liable for the option. This opens them up to extreme risk. If a market maker sells an option with a 50 delta, they are effectively short 50 shares of the underlying equity. Because of banking regulations, most market makers must look to minimize their risk. To do this, the market maker will buy 50 shares of the underlying equity. Since they were previously short 50 shares from selling the option, the process of buying 50 shares of the underlying equity, allows them to become what is referred to as “delta neutral.”

Since stock prices are dynamic and change frequently, the underlying options, and therefore their “Greeks”, are also dynamic and change frequently. Because of this, market makers must also adjust their deltas. The most common form of adjusting deltas is referred to as “Gamma Hedging.” As discussed previously, gamma is the change in delta per change in underlying equity price. 

### MOVE Index

The MOVE Index measures the volatility in the US Treasury market. Essentially, it is the VIX for the bond market. We believe there is a relationship between volatility in the equity market and volatility in the bond market. Because of this, we have included it in our model. 

### Dollar Index (DIX)

The Dollar Index is also a measurement via Squeezemetrics. The DIX measures dark pool short volume, as reported by FINRA in their REG SHO daily files. DIX is calculated by the short off-exchange volume divided by all off-exchange volume. We believe DIX may show some predictive value in measuring volatility and have added it to our model. 

### VIX Term Structure

While it is not possible to trade the VIX at spot prices, it is possible to trade VIX futures. Since VIX trades off of futures, there is a term structure. A term structure refers to the value a futures contract trades off based upon the month. For instance, you can buy a December VIX future contract, as well as a July VIX contract. Since they are two separately traded instruments, they have two different prices. There are two possible states for the VIX term structure to be in. These states include “Contango” and “Backwardation.” Contango refers to nearer-term VIX futures being cheaper than longer-term VIX Futures. Conversely, backwardation refers to nearer-term VIX Futures being more expensive than longer-term VIX Futures. Historically, when volatility increases the state of backwardation occurs. 

For our model, we want to test what effect contango and backwardation play on volatility, as well as the degree of contango and backwardation play. 

Below is a chart that shows VIX term structure in contango. This is related to a lack of volatility in the markets.

 


In comparison, below is a chart of the VIX term structure in backwardation. This is related to an increase in volatility. 

 


### Project Background

 
The above chart shows the relationship between dealer’s Gamma Exposure and the S&P500 daily change. The graph shows that as gamma decreases, volatility (SP500 change) increases. The opposite is also true, as gamma increases, volatility tends to decrease. From the graph above, orange dots represent days where the market was positive, and the blue dots indicate the market being negative. Days where gamma is higher, tend to lead to more positive days, while lower gamma tends to be more negative. 

 
The above chart is the return of the S&P500 returns in absolute terms. Since we are focused on volatility, we are uninterested on determining the directional move in the markets. This graph further illustrates that lower gamma leads to increased volatility. Due to what the above two graphs show we believe we can find a relationship between Actual Realized Volatility and Gamma Exposure. Our goal is to find the relationship, and then see if we can compare that to the Implied Volatility to gain a trading edge.

 
The above chart shows the history of implied volatility to realized volatility. As you can see, a majority of the time implied volatility exceeds the actual, realized volatility. This is due to there always being a need for “insurance” on underlying equity positioning. Because of this, we say that volatility trades as a premium. This premium is the spread between implied and realized volatility. From the charts, we see that selling volatility is a great strategy until it is not. The two major volatility events, 2008 Great Financial Crisis and the 2020 COVID-crash, were examples of when volatility sellers struggled mightily. From the chart above, the average spread between implied volatility and realized volatility is about 45 basis points (0.45%). 

The above chart shows the basis of our project. We want to create an implied volatility metric that shortens the spread between implied volatility, but also doesn’t blow out when a major volatility event occurs. 

### Model Results

The first model we ran, is a Random Forest Regression (RFR) model. We chose this model, because RFR models do a great job at explaining which variables are important in determining the predictive values of a model. We would then take those insights and try to build a better model from there. We ran through the modeling process and the RFR returned a score of 0.7554. This is a pretty good score for our first attempt. The model returned an RMSE of 0.00708.          
From the above chart we were able to make observation on the various features of our model that gave us predictive capabilities. The most predictive variable from our model was the previous close of the Volatility Index (VIX). The next most important variable is the Gamma Exposure of dealer positioning. This confirms are previous hypothesis stating that Gamma Exposure determines a large part of volatility. 

Our next step in our modeling process was comparing our model’s implied volatility to the VIX as well as the actual realized volatility of the market. For this, we took our model’s volatility predictions and subtracted the absolute realized volatility of the market. We did this for the VIX’s implied volatility. From this we were able to find the difference, or spread, from the implied volatility and realized volatility. If implied volatility perfectly predicted realized volatility, the spread would equal 0. 

 
The above chart shows the spread between our model’s implied volatility and actual realized volatility. The average spread between the two throughout this time period is about 0.483%. 

 
The above chart shows the spread between the VIX’s implied volatility and actual realized volatility. The average spread between the two throughout this time period is about 0.643%. 

The two charts above show the relationship between our Model's predicted volatility vs the actual volatility of the markets and the relationship between the VIX's implied volatility vs the actual volatility of the markets. As discussed in the previous model above, there is usually a premium to volatility as realized volatility doesn't exceed the implied volatility. The difference in implied vs. realized is measured in a spread. The goal of this project is to minimize the spread between a predicted or implied volatility, and the actual realized volatility. These graphs show that our model was able to do just that. By the prediction stats, we see that the average spread between our model's implied volatility and realized volatility, is by about 48 basis points. This is compared to the VIX's average spread of about 64 basis points.

From the charts above, we can see that our model has done a better job at modeling volatility compared to the VIX. From here we need to understand where our model differs from the VIX. 

 
 

The two charts above show the relationship between our model's Implied Volatility and the VIX. When the line is below 0, our model believes that the VIX's implied volatility is too high, and one should short the volatility. When the line is above 0, that shows that our model believes volatility is too low, and one should be buying volatility. It is interesting that our model believes that the VIX is usually expensive as it spends a majority of its time below the 0 level. As we look at trends in the charts, we see that our model saw big advantages in the volatility markets both before and after the COVID crash in 2020. Looking at recent trends we see that shorting volatility is getting less and less attractive.

### Market Liquidity vs Volatility

For the model below, we wanted to see what the effect of Top of Book Liquidity would have on volatility. We hypothesize that the less liquidity there is in markets, the more volatile the market is. Unfortunately, data for what we are trying to model here is very hard to obtain. Top of Book Liquidity data via the Chicago Mercantile Exchange (CME), was going to cost ~$19k if we wanted to capture the data that goes back to the May 31, 2011, start date in our other data collected above. Fortunately, the CME provides 2-year sample data we were able to use to at 
least get a fraction of our time period. The results from that data are below. The chart below illustrates the liquidity of the S&P from the last 2 years. The wider ranges indicate a more liquid trading market. As one sees, the market has been less liquid over the last year. 

 

To test out the impact that liquidity has on market volatility, we again ran a Random Forest Regression model on our data. The accuracy of the model wasn’t as great as the previous model, as we got a model score of 0.6957. The interesting insight we can take from this model is the results we received in the feature importances. Below we have a chart of the model’s feature importances. 

 
According to the model, the liquidity levels (TOB Rolling) was the most important factor in determining the volatility of the market.  

All in all, there are several interesting ideas to take away from this model. The model had an RMSE score of about 0.7, which is slightly less than the previous model's score of about 0.75. One of the key takeaways, from this model is that the time snapshot of the data we were able to obtain, did not feature the major volatility events of 2008, 2018, or 2020. It would have been interesting to see what factor liquidity levels would have had during those highly volatile time periods. Next, we can see that through the feature importance tool that our hypothesis was correct in believing that the liquidity, measured by the Top of Book liquidity level, was a major factor in determining the levels of realized volatility. As liquidity decreases, the level of volatility increases, and vice-versa. Another key takeaway here, is just the general fluidity and ever-changing mechanics of the stock market. On our previous model, factors such as the various VIX measuring instruments played a much more important role in determining volatility. In this much narrower model with less data, factors such as treasury market volatility (MOVE) were more central to determining market volatility. This coincides with the overall Treasury Market weakness we have experienced for a large part of 2022. We believe that had we had data that would have spanned the course of the major 2008, 2018, and 2020 volatility events, this feature importance model would have placed more emphasis on our various VIX measuring metrics.

Once again, we wanted to see the features that were most predictive in determining volatility, so we decided to run a Random Forest Regression model. This model was our most accurate model as it had a score of 0.7746. The model had an RMSE of 0.00695. Below is a graph of our feature importances. 

 

As the above chart shows, the spread in term structure (degree of contango/backwardation) plays a major role in determining the volatility of the market.

### Conclusion 

### References 
1. Options basics: https://www.optionsplaybook.com/options-introduction/options-basics/
2. Option Gamma Exposure : https://www.youtube.com/watch?v=jfTFMlotrjc
3. Implied Volatility and Options : https://www.youtube.com/watch?v=Q3XAlfAyMGI

### Team Members
1. Drew Haggerty
2. Billel Loubari
