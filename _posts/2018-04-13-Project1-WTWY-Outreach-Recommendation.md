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

What day or days shall the street teams go visit the stations? We summed the top 10 stations traffic by day, then took the average to visualize the best days in the month of May to get signatures. Wednesdays and Thursdays tend to be busier than other days, and a lot more than weekends as commuters would work on weekdays. 

![alt_text] (https://github.com/mizhao2018/mizhao2018.github.io/blob/master/_posts/Busiest%20Days.png)

What about hours? What are some of the best times to send our street teams? We binned the time to 4-hour blocks to see if we can find a pattern. Additionally, we've added weekday to the date, as "0" represents Monday, "1" for Tuesday, and so on. The morning and afternoon rush seem to be good times in terms of foot traffic. 

![alt_text] (https://github.com/mizhao2018/mizhao2018.github.io/blob/master/_posts/Busy%20Times.png)


## Is foot traffic all we care about? 
Foot traffic cannot be everything that one looks at. After all, us as data scientists should look beyond the obvious data and discover insights! How can we make this project easier for the street teams? In addition to the crowd at Penn Station, what if people are too busy to stop to hear about the organization? 

In lieu of this, we thought about coffee shops. People who get their morning cups of coffee will be more at ease to listening to a marketing pitch. In addition, Starbucks as a brand is more prestigious so their customers are more likely to be more well-off (compare to people who frequent other coffee shops -- note, this is an assumption). Therefore, we found the number of Starbucks within 0.3 miles of the station, and ranked the existing 10 stations based on the number of Starbucks. 

Together with income data, tech funding, and Starbucks, we ranked the stations from 1-10, with "1" being the best station to visit. 

![alt_text] (https://github.com/mizhao2018/mizhao2018.github.io/blob/master/_posts/Ranking%20Data.png)




