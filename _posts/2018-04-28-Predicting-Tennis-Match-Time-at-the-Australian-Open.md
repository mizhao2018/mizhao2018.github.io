---
layout: post
title: Predicting Tennis Match Time at the Australian Open
---
Australian Open, the first Grand Slam of the year, millions of people tune in to watch the tournament take place in the beautiful city of Melbourne, Victoria. For spectators in the US Melbourne is half way across the globe, so catching a match is not always convenient in terms of timing. Granted, nowadays, almost everyone has Tivo to record all the actions, but watching a match the next day misses all the excitement. If we know when the previous matches will last before we go to bed, then we can predict when we should get up, and consequently, stay up for, that once in a lifetime Roger Federer vs. Rafael Nadal match (assuming these guys play in earlier rounds). Can I build a model to predict the length of a tennis match in the Australian Open? 

## Gathering the Data
To acurately predict the match time, I gathered three types of data. Singesl match information from Australian Open 2018 as my base data, player ranking (April 2018) as a proxy for that in January 2018 since only a handful of ATP has taken place so far, as well as weather information of Melbourne in January 2018. Melbourne can have 4 seasons in a day, and January is no exception. The problem is that it often gets so hot that players have to take longer breaks, so I wonder if that has an impact on player performance, and eventually, match time. 

## Feature Selection
From an intial glance of the data, we have information such as: 
* Player rankings
* Scores
* Type of match - Men vs. Women, Singles vs. Doubles
* Court information - Rod Laver, Margaret Court, Hisense Arena, Show Court, etc. 
* Match outcome - complete, retired
* Day match was played 
* Round information - 1st, 2nd, etc.

It's easy to include all the information, but information such as "scores" is an outcome of the match. If I am predicting the match time, I should not be using another outcome of the match as an input since, I wouldn't have known the scores if the match has not taken place yet! 

The final list of input variables listed below: 
* Player Rankings
* Type of Match - Men and Women Singles only
* Type of Court - categorized into: Stadium (Rod Laver, Margaret Court, Hisense Arena), Show Court, and General Court
* Temperature (in Celcius) 
* Round Information
Note - I also only included completed matches, so a total of 253 matches over the course of 14 days became my dataset! 

## Modeling
Part of the fun as a Data Scientist is to derive a model that can best answer the question. Without getting too deep into weeds, I divided my data into 80% train and 20% test. I started with a simple Linear Regression with SK Learn, but reazlied that I can try polynomial as to allow some features to interact, for example, how does temperature affect men vs. women matches? 
![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/004.png?raw=true)
That resulted in overfitting, and I have more than 100 variables! 
From there, I went ahead with Regularization (tried Lasso and Ridge), a technique to prevent overfitting by augmenting the cost function. With four models in hand, I compared the Mean Absolute Error (a way to measure model effectiveness) on the validation set of my training data and decided that the model with Lasso regularization works best. A lot of jargon... 
![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/006.png?raw=true)

## Ok, technicals aside, how good is my model? 
My model can predict a match time with +/- 30 minutes. It is not the best model, but a good start. For example, the match between Rafael Nadal and Leonardo Mayer during the 2nd Round lasted 2 hours and 38 minutes, while my model predicted it to complete in 2 hours 23 minutes.
![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/007.png?raw=true)
Technically, there is no clear sign of heteroscedasticity based on the residual graph below.
![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/008.png?raw=true)

## What can I use the model for? 
To an amateur data scientist like myself, a model is never practical unless it gives me some applications. Luckily, this model can be used for stadium planning. Match coordinators can adjust the sequence of matches and their courts so that matches can finish before sunset, especially in earlier rounds. Additionally, for fans in the Americas, this model can be used to tune their sleep schedule if they want to watch a specific match. 

## Can you do better? 
It would be interesting to separate men and women's matches and establish 2 different models as men play 3 best of 5 and women play 2 best of 3, so there is some clustering of men vs. women. Additionally, a more robust model would incorporate doubles match as well. 
For now, save up and plan for a trip to Melbourne in January 2019. 
