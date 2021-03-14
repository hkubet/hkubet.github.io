---
layout:     post
title:      Group Project Update 2
subtitle:   Obstacles to be tackled
date:       2021-02-29
author:     Brad, Jessie
header-img: img/blog2_img.png
catalog: true
tags:
    - NLP
    - Wallstreetbets
    - subreddit
---


## Project status

The project is running relatively smoothly at the moment.
![img](/img/Status.png)
We are about 50% done with the project report, where we kept track of progress and accounts.

The web-scraping code is 90% done, we're going to use this code to scrape the WSB subreddit recent threads and comments to obtain the raw data for our analysis. The core tools we plan to use are pushshiftAPI from psaw and praw. PushshiftAPI provided a search by date function, an important tool as we would want to define the exact period.

```
    api=PushshiftAPI()
    result = api.search_submissions(*input parameter)
```
![img](/img/pushshiftapi.jpg)

![img](/img/psapi.png)

The other difficulty we met during web-scraping has something to do with time format. The comments from reddit are running 24/7，but the stocks are only traded during trading hours in business day. Hence we need to organize the comments in the timestamp that is applicable to to our trading data. To do this, we used the pandas Bday and Hday functions. The displayed code can also distinguish trading hours from non-trading hours by utilizing the pandas dataframe function.

![img](/img/pandascode.jpg)


 This whole Reddit-GameStop saga only happened for less than 2 months, hence there is relatively insufficient textual data compared to the regular database. The key thing to note here is the scraping process would be on-going. As time goes by, our data grows with it; we treasure every new thread and comments tremendously as that could potentially change the outcome of our result drastically. Also, scraping other subreddit such as r/thetagang could increase our data size significantly.

 As for the sentiment analysis, the process is close to 70% done, as we have already figured out the process for data cleaning.
 ```
    word_tokenize(text)
    stop_words = stopwords.words('english')
    stemmer = PorterStemmer()
```
  However the most important for sentiment analysis is finding the best dictionary that applies to our data. Reddit is one of the most intricate parts of internet discussion; the internet language used by these 'redditer' is the most in-line with the current trend of the internet. This makes finding a perfect dictionary for analyzing Reddit incredibly difficult as the existing dictionary could not possibly follow these 'hot' topics constantly and update themselves. The most straightforward way to analyze the result would be NLTK VADER, the polarity score could directly reflect the aggregate sentiment of certain sentences, and it is considered a very viable choice for social media sentiment analysis. Loughran MacDonald's word list got its reputation by applying it to financial statement analysis, however, its application in internet language is limited. We're still exploring multiple opportunities to increase our analysis accuracy.

  We are also deciding if implied volatility is the best parameter for the project. On the one hand, implied vol seems to be a straightforward and easy-to-get parameter; on the other hand, it directly links to the price of the option and might not best represent the market risk at such special times.

We expect the project to be finished by March the 13th; it will give us enough time to reflect and refine the project report.
