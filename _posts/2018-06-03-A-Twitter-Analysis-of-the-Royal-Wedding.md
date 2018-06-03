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

Because Twitter is a great platform to use emojis, I made sure that my cleaning will not take out the emojis that people use in the tweets. Interestingly, some Chinese, Korean, and Japanese (CKJ) characters share some similarities with emojis, so I made sure that CKJ characters are removed but emojis are kept. 
 

