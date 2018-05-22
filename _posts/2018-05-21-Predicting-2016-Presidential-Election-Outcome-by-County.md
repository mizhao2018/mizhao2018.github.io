---
layout: post
title: Predicting 2016 Presidential Election Outcome by County
---
The 2016 Presidential Election was an event that few can forget. I remember staying up until 2am to watch it on CNN while on a business trip to New York. To me and many of my friends, the outcome was a surprise to say the least. One of the key reasons for the surprise was the deviation from prediction, from many sources, that Hillary would become the first female President. In the face of facts, data analysis seemed weak. People started to reflect on what "went wrong" in the prediction, and others claim that data failed us. With all of this information in mind, can I predict election outcome by county using county-specific demographic information? 

## Data Overview
From OpenDataSoft, I obtained the dataset that consisted of counties, voting outcome, as well as county-specific socio-economic data. With some initial data cleaning (took out ones without 2016 votes) and filled in null values on some of the features, I ended up with 3111 counties, with Clinton took 486 and Donald won 2625. Point of reference: [the Associate Press reported that Clinton won 487 counties and Trump won 2626 counties.](https://apnews.com/fb5a5f7da21d460bbffb6985cb01cb2c/trending-story-clinton-won-just-57-counties-untrue) 

In terms of the features, the original dataset included information such as Education, Healthcare, Crime, Economic, Occupation, as well as Demographic, so I decided to keep these in my analysis. The original dataset also featured climate information, and previous presidential election outcomes, but I did not consider them as I wanted to focus on key socio-economic features. 

## Data Modeling
As part of one-hot encoding, I made Democrat = 1 and Republican = 0 for the voting outcome. One of the major discussion post-election was focused on false positives. That is, there were counties that were projected to vote for Clinton but actually voted for Trump. These counties, in the statstical terms, are called "false positives." With this in mind, the metrics I am evaluating my models with is **precision**, which is expressed as: 

True Positive / (True Positive + False Positive). 

Models with high precision will have few numbers of False Positives. I ran five different models with 30/70 test/train/split, including: K-Nearest Neighbors (KNN), Random Forest, Kernel RBF, Polynomial SVC, as well as Gaussian Naive Bayes. It turns out that the Kernel RBF with C=80, gamma = 0.001 (through GridSearch) gives the best model in terms of Precision for the Democrat and Republican outcomes. 

![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/P3_ModelComparison.png?raw=true)

Using the Kernel RBF model, I predicted the outcome for ALL of my dataset - 3111 counties in total. Using [Plotly](https://plot.ly/#/), I put the soft-prediction, means the likelihood of the county voting for 1 (Democrat) in the county map. Counties with dark red are more hard-core Republican, whereas counties with solid blue are more pro-Democrat. 

To be a little more nerdy, I wanted to see how many counties did we predict wrong, both on the Republican and the Democrat sides. This histogram represents the number of counties voted for each party, with the x-axis showing the predicted likelihood of voting for Democrat (again, 1 = Democrat, and 0 means very Republican), and y-axis (bar height) representing the number of counties that **actually** voted for each party. Why is this important? To zoom in on the section in which probability of voting for Democrat is greater of equal to 0.5, we see some red bars underneath, and these are the counties that analysts predicted to vote for Clinton but won by Trump. *These* are the false positives, and the ones that perhaps, people wrongfully hoped for. 

<iframe src="https://plot.ly/~mizhao2018/10/?share_key=SAuBNVpDX16ZImXw6jWJu4" width="850" ></iframe>

To be more precise, the confusion matrix demonstrates the split bewteen true positive, false positive, true negative, and false negative. What I am interested in are the 12 and 37 - which are the false positive, and false negative, respectively, on the test set. To tie it together, these are the numbers that we strive to minimize. 

![alt text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/images/P3_Confusion.png?raw=true)

## A twist in Data with Monte Carlo Method 
Having all of the models and some generalization, I wanted to see if these factors are just coincidentally so made these counties vote for R/D? In other words, if I shift the figures a little bit (say, increase income by 5%, or decrease physical sick days by 0.5 days), will the county be "loyal" to their initial pick? 

I went ahead with generating a dataset with 1000 sets of values using the Monte Carlo method. Taking the mean of the each feature, I added a noise with a normal distribution of standard deviation of the feature. For example, if the mean of median income across all 3111 counties were $50,000 and standard deviation of $3500, then the new 1000 sets of data on income = $50,000 + noise, where noise follows a normal distribution of (50000, 3500). Running 1000 values through the Kernel RBF model, I calculated the probability that each county will vote for Democrat, and visualized it on the county map. Where you see darker red means the counties are very pro-Republican, and that some variation in socio-economic information will **not** likely to impact on their voting outcome (same as dark blue for Democrats). The interesting counties are the ones that have the lighter shades, as shown here to be some of the Midwest, and West Mountain regions. These are the areas in which with some change in features, the outcome might shift. Even though this was a priliminary analysis, focused ONLY on the county's information and not taking in polls, we can already see some possibility for campaigns or social changes to impact election outcome. 

You can see my Monte Carlo Simulation here. Note, you can also hover over each county to see the likelihood.

<iframe src="https://plot.ly/~mizhao2018/14/?share_key=gR4GjjS0q1D9boMRXcmxpE" width="850" height="850" ></iframe>

## So what's next? 
Post eletion, there were many analysis done on the correlation of certain attributes to people's voting behavior. There are two things that I am particularly interested in: [Cracker Barrel and Whole Foods](https://twitter.com/Redistrict/status/796425128359972864), and [health data](https://www.economist.com/news/united-states/21710265-local-health-outcomes-predict-trumpward-swings-illness-indicator) in relation to election outcome. I'm hoping to look into the analysis in these claims and prove their truthfulness (if true). 

## My final thoughts
When I first started this analysis, my only motivation was to see if I can observe a pattern in county's voting behavior. As I became more involved in data collection and modeling, I realized that there's a moral to every data analysis, and that is: 
*As Data Scientists, we should have a full grasp of our data limitations and the potentially flawed assumptions that we make to build models as to better adjust and understand the applicability.* 

As good as my model claims to be, it will most likely be unapplicable in three years as so many other factors play a part in this process. My best hope is that we take careful consideration of our models, assumptions, and claims, so to be responsible for the analysis that we make and the ramifications thereof. 
