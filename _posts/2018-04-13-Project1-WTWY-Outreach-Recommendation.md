---
layout: post
title: WomenTechWomenYes - Fundraising Outreach Recommendation
---

WomenTechWomenYes is a non-profit organization that encourages females to pursue careers in technology. They reached out with regards to creating a strategy for their annual gala that will be held in the summer. Our team at Metis was tasked with using MTA data and additional data source to help the marketing team with this effort. 

## First Impression of Data
As a previous technology consultant, I am comfortable with Excel and SQL. However, doing data processing in Pandas and Python was completely new to me, but it was also thrilling to know that these tools can be very powerful with large datasets. So, here we go. 

MTA turnstile data is organized by week, so initially we downloaded one week's data and checked out the information given. Without much background in MTA turnstiles or New York subway lines, we resorted to a data dictionary to understand more about the data. The ENTRY and EXIT data are presented in cumulative form, so we will need to obtain daily or hourly foot traffic data for future processing. 

## Data Cleansing
One of the most important aspect of a data scientist (from my few weeks of experience as a Data Analyst at the CME Group) is to conduct analysis with a clean set of data. At the same time, depending on the data presented, this is also one of the most challenging steps for any beginner with a new programming language. Without going into the details, here are some of the key steps we took with the MTA data. 
* Grouped "A/C," "UNIT," "SCP," and "STATION" as one unique entity so we can look at the data collectively;
* Created "hourly_entries" from cumulative ENTRY data;
* Deleted "hourly_entries > 5000" since the difference beyond 5000 comes from differences from different entities, and not within one entity.
* Deleted "hourly_entries < 0" for similar reason as above. 

Note*: We did not compute the daily_exits data because exits at some stations are not tracked, so the data presented in the dataset is not consistent. 

## Which data is interesting?
As this is our first project, we decided to tackle one question at a time, starting from the most basic question - what are the busiest stations by entrance count? 
After we found the stations, we pinpointed the stations on a map to visualize better. Not surprisingly, most of the stations are centered in lower Manhattan and Wall Street. 

![alt_text](https://github.com/mizhao2018/mizhao2018.github.io/blob/master/_posts/Top%2010%20Stations.png)
