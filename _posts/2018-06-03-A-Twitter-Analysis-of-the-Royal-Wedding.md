---
layout: post
title: The Royal Wedding of 2018 - A Twitter Analysis
---

Even though England has been a constitutional monarchy since 1689, anything related to the Royal Family always attracts the public eye. Recently, the Royal Family has portrayed itself as an entity that is more open to the public, especially with the new generation of the family that is younger and more energetic. Not surprisingly, people around the world are drawn into big events surrounding the yet mysterious family, especially when it is the wedding of the prince, marrying Meghan Markel, someone who comes from a very different background yet so special to the family as a whole. 

My emotions aside (Meghan graduated from **my** alma mater - Northwestern University), I wanted to see if I can use Twitter data to analyze what people talked about during, and after the wedding, as well as people's general emotional state towards the new couple & the Royal Family. 

## Twitter Streaming
Setting up the tweepy (a tool to access Twitter API through Python) and mongoDB has been probably the most fun part of this project. Knowing that I would be capturing the twitter feeds live as they come in, I can really feel the power of technology. In order to have uninterrupted streaming, I set up tweepy and mongoDB in my AWS EC2 instance (virtually) so whatever I do on my local machine will not impact on progress being made. Throughout the day, I would query the number of tweets stored in mongo as feeling a sense of accomplishment. Unfortunately, Twitter's unpaid plan will only give me a SAMPLE of the tweets; however, after +3 days of streaming, I captured almost 1 million tweets, which is sufficient for my studies. 

## Python & Mongo
Few days after the wedding, I started the analysis part. Building a connection between Python (on my local machine) and Mongo on AWS has been a fun journey, thanks to a post by [Ian London] (https://ianlondon.github.io/blog/mongodb-auth/), who explained the process in great detail. *Note, please read comment 1 in the post to make modifications from the instruction as that took me +2 hours to solve!* With successful connection, I was able to build a dataframe that contained all the tweet information that I collected, including text, user name, location, time posted, as well as device (if available). 

Using some of the natural language pre-processing techniques, I cleaned, stemmed, and tokenized the tweets, leaving only English / phonetic characters. For example: 

*Original text* "Meghan Markle's Dress looks amazing! What a beautiful & magical wedding! #royalwedding" 

*Processed text* 'meghan','markle','dress','look','amazing','what','a','beautiful','and','magical','wedding','royalwedding'

Because Twitter is a great platform to use emojis, I made sure that my cleaning will not take out the emojis that people use in the tweets. Interestingly, some Chinese, Korean, and Japanese (CKJ) characters share some similarities with emojis, so I made sure that CKJ characters are removed but emojis are kept. I used n-grams = 3 to make sure the words that I keep actually do have meanings. Unfortunately, none of the emojis made to the top 2000 frequently used words! 

## Topic Modeling
Using different techniques (LSA, NMF, and LDA), I came up with 5 top topics from the tweets. With some context, I think that the NMF model gives the most reasonable topics, namely:
* Wedding & Queen
* Guests (Clooney, Beckham)
* Congratulations Meghan & Harry
* The Royal Family, and 
* Bishop Curry's Sermon & Love
![alt text](https://raw.githubusercontent.com/mizhao2018/mizhao2018.github.io/master/images/Project4_Presentation.004.jpeg)

On a side note, I am so glad that Bishop Curry's sermon made it to the top 5 topics list. Listening it live was a complete refreshner for the traditional British Royal Wedding; however, this whole time, I wanted to see the reaction from the Royal Family and what they really think of this American bishop! He was bold, passionate, and funny! I totally loved it because it was so different, inclusive, and very true. 

In terms of when people tweeted, I segmented the 3 days into 3-hour blocks, starting the day of the wedding. Since all times are in GMT, the time corresponds to the wedding. Not surprisingly, most tweets were published during the wedding, and as the day goes on, the tweets starts to dwindle as well. Most people talked about the Wedding & Guests, but right after the wedding, the attention was more on the wedding itself and the Queen. 
![alt text](https://raw.githubusercontent.com/mizhao2018/mizhao2018.github.io/master/images/Project4_Presentation.005.jpeg)

## Who's Tweeting?
As this is one of the most watched weddings, people from all over the world tuned in through streaming or even the social media. In fact, Northwestern Alumni Group in London hosted a "watch party" and held their flag high when Meghan's coach was driving by. It was quite amazing. ![](http://www.trbimg.com/img-5b009990/turbine/ct-1526765965-jt7h6cnmhj-snap-image/640/640x360) 

With location information, I categorized the tweets in three groups: US, UK, and the world. I also performed a sentiment analysis on how happy people were in their tweets. Note, sentiment analysis was done using TextBlob, and as that is mostly applicable with movie review, this might not be the best tool to evaluate spectators' state of mood. Also note, the number of smily faces do not represent the scale of happiness, rather, it was an indicator to show that the UK was happier than the US, followed by the rest of the world. 
![alt text](https://raw.githubusercontent.com/mizhao2018/mizhao2018.github.io/master/images/Project4_Presentation.008.jpeg)
 
## What about gifs and memes? 
Throughout my anslysis, I saw many external links in the body of the text. These links are primarily memes or gifs that are contain a lot of messaging. My favorite was the gif on Harry's first words to Meghan: "You look amazing. Are you ok?" Emotions aside, if I could decipher these non-verbal expressions, I might be able to extract more meaning, and perhaps, more topics, from these tweets. 

## What's next? 
As cheesy as it sounds, I am hoping to see the Duchess of Sussex one day when she returns to Northwestern. I promist I will do a curtsey. All the best, Meghan & Harry! 
![] (https://static01.nyt.com/images/2018/05/20/world/20royalwedding-photos27/merlin_138381726_9146ba9a-cb25-4c29-8d05-0fc9f1033302-superJumbo.jpg)
