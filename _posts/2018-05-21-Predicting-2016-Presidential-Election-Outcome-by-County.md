---
layout: post
title: Predicting 2016 Presidential Election Outcome by County
---
The 2016 Presidential Election was an event that few can forget. I remember I stayed up until 2am to watch it on CNN while on business trip to New York. I think to me and to many of my friends, the outcome was a surprise to say the least. One of the key reasons for the surprise was the deviation from prediction, from many sources, that Hillary would become the first female President. In the face of facts, data analysis seemed weak. People started to reflect on what "went wrong" in the prediction, and others claim that data failed us. With all of this information in mind, can I predict election outcome by county using county-specific demographic information? 

## Data Overview
From OpenDataSoft, I obtained the dataset that consisted of counties, voting outcome, as well as county-specific socio-economic data. With some initial data cleaning (took out ones without 2016 votes) and filled in null values on some of the features, I ended up with 3111 counties, with Clinton took 486 and Donald won 2625. Point of reference, [the Associate Press reported that Clinton won 487 counties and Trump won 2626 counties.](https://apnews.com/fb5a5f7da21d460bbffb6985cb01cb2c/trending-story-clinton-won-just-57-counties-untrue) 
