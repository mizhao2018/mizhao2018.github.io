---
layout: post
title: Predicting Tennis Match Time at the Australian Open
---
Australian Open, the first big Grand Sland of the year, millions of people tune in to watch the tournament take place in the beautiful city of Melbourne, Victoria. For spectators in the US, Melbourne is half way across the globe, so catching a match is not always convenient in terms of timing. Granted, nowdays, almost every has Tivo to record all the actions, but watching a match the next day misses all the excitement. If we know when the previous matches will last before we go to bed, then we can predict when we should get up, and consequently, stay up for, that once in a lifetime Roger Federer vs. Rafael Nadal match (assuming these guys play in earlier rounds). Can I build a model to predict the length of a tennis match in the Australian Open? 

## Gathering the Data
To acurately predict the match time, I gathered three types of data. Singesl match information from Australian Open 2018 as my base data, player ranking (April 2018) as a proxy for that in January 2018 since only a handful of ATP has taken place so far, as well as weather information of Melbourne in January 2018. Melbourne can have 4 seasons in a day, and January timeframe is no exception. The problem is that it often gets so hot that players have to take longer breaks, so I wonder if that has an impact on player performance, and eventually, match time. 

## Feature Selection
From an intial glance of the data, we have information such as: 
* Player rankings
* Scores
* Type of match - Men vs. Women, Singles vs. Doubles
* Court information - Rod Laver, Margaret Court, Hisense Arena, Show Court, etc. 
* Match outcome - complete, retired
* Day match was played 
* Round information - 1st, 2nd, etc.
