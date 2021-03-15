---
layout:     post
title:      Group Project Final Update
subtitle:   Final form of our project
date:       2021-02-29
author:     Brad, Jessie
header-img: img/blog2_img.png
catalog: true
tags:
    - NLP
    - Wallstreetbets
    - subreddit
---


# Updates

Our project is very close to being finished. Our group made some changes since the last update, for example, we discarded the implied volatility as our main parameter and used stock return instead. The main reason to use stock return is that implied volatility would change vastly when the strike price of options change. The strike prices of options on the same underlying can vary significantly，causing some options that are deep in or out of money almost impossible to be exercised. As a result, the implied volatility could be a biased indicator in evaluating the impact from text sensitivity on social media. In addition, we added a trading strategy based on our results; the trading strategy is relatively compelling with linear regression as support and provided a further application for our discovery.

# Data Processing

-	How to categorize comments on trading days and non-trading days

These are the functions that can be used to define whether a date is a business day or a holiday. Because the trading days are business days and non-holidays (business days only include Monday to Friday while excluding some holidays that are within the week), we separate comments data into non-trading and trading days so that we can do regression according to different timeframes.

![img](/img/blog3p1.png)

-	This piece of code set the Trading Hours between 9:30 to 16:00 during Eastern Time Zone.

For the df_comment[‘Date’] piece of code, if the comment is generated after 4pm (Eastern Time), then it’ll be categorized to the next working day hours.

For the df_trading piece, it selects the comments from 9:30am to 4pm (Eastern Time) on working days.

![img](/img/blog3p2.png)
![img](/img/blog3p3.png)
![img](/img/blog3p4.png)


-	How we calculate the three different kinds of sentiment scores:

1. Reddit comment score - weighted score: the number of upvotes extracted earlier in the scrapped data, presenting the influence of the submission. The more upvotes one submission receives, the higher weight it gets.

2. Log_Reddit comment - score: scaled by the logarithm function: for every comment score, it is applied with log10 divided by the sum of the logged comment scores. This method assigns submission or comments with significant upvotes not as much weight compared to the Reddit comment score-weighted strategy.

3. The equally weighted score strategy assigns different submissions and posts with the same weight.

![img](/img/blog3p5.png)

# Trading Strategy
After discussions with Dr. Buehlmaier, our group has decided to act on our final results and added a trading strategy. After closely looking into the data, we found two statistically significant factors relating to the GME stock return. We tested a bunch of trading strategy that worked well under these circumstances, but we still think it is best to have statistical evidence to support to make the strategy more compelling

## Trading Hours Sentiment
The first of our findings is “Trading Hours” upvote-weighted sentiment and stock return in the same period. The set of parameters was inversely correlated with a p-value of 7.8%; however, in practice, it is physically impossible to collect all the sentiment of the day and trade the stock at the beginning of the day (We’ll have to go back in time to execute such trade). This is more like a post hoc analysis; to find a “predictive” factor, we will need factors that can be found in the historical information.

![img](/img/blog3p6.png)

The regression result is shown below.

![img](/img/blog3p7.png)

## Non-Trading Hours (average of Lag1+Lag2) of GME
After looking closely at our data, we found that the average equal-weighted sentiment for the past two days also has a statistically significant relationship with the stock return in time t +1(ie, an average of t-1 and t-2 non-trading hours sentiment might be correlated with the return from t+0 to t+1). This pair of parameters has a p-value of 6.7%. The result could indicate the sentiment in the previous two days is correlated with the stock return for today. This factor is advantageous as it is a lagging factor that can actually be applied in the trading strategy.

![img](/img/blog3p8.png)
![img](/img/blog3p9.png)   
The regression result is shown below.
![img](/img/blog3p10.png)
# Future Improvements
### Data Size
One of the biggest problems we ran into was the data size. This event only happened for less than 2 months, the amount of useful information is extremely limited. This might cause a couple of problems. Other than that, r/wallstreetbets has much more saturated data in this stock (GME) than the other 6 stocks we investigated earlier. The number of the rest of stocks’ comments is simply not enough for analyzing sentiment or they might be lacking for comments for a few days in between, creating a gap in the input data.
To start with, the small data size might limit the reproducibility of our model. A good model has to be back-tested for a long period to see its reliability. In addition, our strategy might not be applicable to stocks other than GME, as other stocks such as AMC might not have enough sentiment data to be formed into a trading strategy.
As we gather more data from other sources about more stocks, it is then viable for us to add more stocks to our portfolio to execute the trading strategy.
There are two solutions to this problem. To start with, we can simply scrape more information from other subreddit, such as r/thetagang. In addition, we could scrape Twitter for keywords to increase our data size. The second solution is bounded by physics, ie, time. As time goes by, we can not only gain more sentiment information but also stock price information. In other words, our trading strategy can grow with time.
