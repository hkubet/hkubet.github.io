---
layout:     post
title:      Group Project Update 1
subtitle:   Ideas generation
date:       2021-02-12
author:     Jessie
header-img: img/blog2_img.png
catalog: true
tags:
    - NLP
    - Wallstreetbets
    - subreddit
---



## Idea generation

> The best way to have a good idea is to have a lot of ideas.

Prior to the first NLP class, major news platforms were flooded with the GameStop price surge. All of the sudden, Reddit became the central topic of retail investors to rally against big hedge fund institutions. Thus, our idea was inspired by how the WSB subreddit - the retail investors discussion board - impacts stock prices.     

Later on, many institutions joined Reddit and plan to scour forums such as Reddit by natural language processing for risk management. Some social media platforms are now playing a more central role in financial markets to analyze the retail investment position which was historically opaque.

After brainstorming the idea and discussing with the professor, our group’s plan A is to scrap a few main sub Reddit forums and seek correlation between the Reddit sentiment and volatility of corresponding stock prices; the plan B is to scrape tweets from accounts that have over 10,000 followers and analyze whether tweets from influencers would have a major impact on related stock prices.

We started off with WallStreetBets because it is such a big community for retail investing and a lot of people see it as a place going forward to influence retail investing. While scraping WallStreetBets, our group encountered the main roadblock to scrape the historical data.  One potential solution is to install the pullshift package and combine it with the Praw package to acquire more historical data from Reddit.
