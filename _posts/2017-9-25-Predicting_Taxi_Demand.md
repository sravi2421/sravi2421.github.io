---
layout: post    
title: Predicting Yellow Cab Demand
---

*Predicting Yellow Cab Demand Throughout New York City* 

When arriving in New York City several years ago, I was taken aback by how prevalent Yellow Cabs are throughout the streets of New York. They make up a good chunk of traffic on any Manhattan Block. But in recent years, they have experienced increasing competition and decreasing market share as new competitors enter the market.

Following a TLC Freedom of Information Law request, the City of New York began releasing summaries of all yellow cab trips for any given month in the form of a csv file. Using this data, I was interested to see which neighborhoods of Manhattan see the bulk of pick-ups, and to create a predictive model for yellow cab demand given a specific neighborhood and pickup date/time. Equipped with this tool, any cab driver could position himself to optimize revenue.

**The Data**

The data set I used was a summary of all trips logged between July 2015 and June 2016. In total, this included just over 130 million trips over that time frame. These 130 million trips equate to approximately 350,000 trips per day. Additionally, I supplemented this data with weather details on an hourly basis which I scraped from Weather Underground. The raw data set included pick up and drop off location coordinates as well as fare details. Mapped out, pickups throughout Manhattan looked roughly similar to the plot below.  In this plot, I have used a web mercator map projection.[explain graph]

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/bokeh_plot (3).png)

Since I was trying to project taxi-cab demand for different areas of the city, I needed to first create a neighborhood field for each of the 130 million data points.  Using a shape file created by the City of New York, which provides neighborhood boundaries, I was able to place each of the 130 million pickup locations shown abl into one of the over 200 neighborhoods of New York City.  Below is a heatmap of pickups throughout the city.  As expected the vast majority of pickups are occuring in Manhattan and the two major airports of NYC.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/heat_map_yellows.png)

**Modeling Demand**

When modeling demand I focused my attention on the high volume pick up areas within the City: Manhattan and the two major Airports. The target variable I was looking at was total pickups on an hourly basis, and I divided this figure by the square area (square km, calculated via a World Mercator Projection) so that each neighborhood was being considered on an apples-to-apples basis. So for example, one observation was pickups per square km in the Lower East Side between 10 and 11pm on Saturday January 26th, 2015. 

In total, my dataset included 455,460 observations.  Given that most of the variables included within my dataset were categorical I one hot encoded each of these variables. Also given the concentration of categorical variables, a random forest seemed to be the logical choice for my model and after fitting a Random Forest Model to the data, the model performed fairly well, achieving an R^2 of .94.  The features which provided the most predictive power included neighborhood, time of day, and neighborhood type. The two most important features on an individual basis were: Penn Station/MSG and Commercial 2(indicating that a neighborhood had a high density office space). Below is a graph of total feature importance. Keep in mind that each of these features shown below are a summation of each specific category within each variable, many of which are extremely unbalanced. 

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/Feature_importances_categorical.png)

More specifically, you can see here the rankings of individual features.  Interestingly, the two most important features are associated with regions of the city which experience extremely high levels of yellow-cab demand, while the next several indicate times of the day/week when you would expect demand to be decreased.  Surprisingly, weather conditions had very little effect on taxi demand.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/feature_importances_all.png)

Lastly, when looking at the model's residuals, you see that many of the higher residuals are occuring in the Penn Station Neighborhood.  Upon further investigation, I found that many of the under-predictions were coinciding with large scale events occuring at Madison Square Garden.

-  11/25/2015: Stevie Wonder
-  05/01/2016: Pearl Jam
-  11/29/2015: Knicks, Rockets OT 
-  09/07/2015: U2

After seeing these large residuals, I scraped additional data on events at Madison Square Garden and added a feature indicating both the type of event and whether the observation was close to the end or start time of an event. Unfortunately, thise new feature had little predictive power. I think a large part of the problem here is that the events above are truly large scale events which are unprecedented in size.  If I was able to find some measure of attendance for each of these events, I suspect the predictive power of that variable would certainly change the accuracy of the model.

Other large residuals had components which the model would have no way of detecting:
- 2016-01-23/2016-01-24: the weekend of a large blizzard in NYC which caused an emergency traffic shutdown throughout New York City
- Lower East Side, 2016-03-13 02:00:00: the weekend of the St. Patty's day celebration, significantly altering night-life patterns


Visualizing Demand Shifts
With a fairly accurate model, I wanted to put together a generalizable tool for cab drivers to use to guide their routing throughout shifts. Below is a brief video showing the capabilities of the demand prediction engine.  If you would like to toggle with it yourself, you can reach the interactive visualization through the following link: [D3 Visualization](http://bl.ocks.org/sravi2421/raw/aba4b211fcbaea98b2af437e19bb5e72/).


{% include youtubePlayer.html%}

Lastly, for a more pinpointed look at demand, you can see here where the majority of pickups were in the specific time intervals listed below.


**Further Work**

I think the tool I presented here is a good starting point for yellow cab drivers as they compete with their new competitors who are much more data savvy and are better connected with their customers. While the toolset I have presented here gives cab drivers a good sense of where yellow-cabs are being hailed, it has no insight on which parts of the city are underserved. Unfortunately, this is one area in which Uber and Lyft's business model gives them much better insight in to how to best serve their customers. They have access to a much richer dataset which allows them to direct their fleet in a synchronized manner. One way to try and better understand this issue is to look at the introduction of green cabs and examine which neighborhoods benefitted the most from their launch.

Additionally, while the current model gives drivers a rough estimate of which neighborhoods they should head to, I think I could further optimize this problem by splitting the city up into avenues which could provide taxi-drivers more targetted demand estimates. 
