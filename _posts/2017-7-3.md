---
layout: post    
title: MTA Data Exploration
---

*MTA Data Exploration to inform canvassers at WomenTechWomenYes*

The first project for the bootcamp was an exploratory data analysis of MTA turnstile data.  We were given a hypothetical client, WomenTechWomenYes (WTWY), who was about to host a summer gala for their organization, and asked to make recommendations on how they could best place their street teams outside the city's subway stops to target potential attendants. Before getting into the details of our analysis I'm going to outline our assumptions for the event and how we defined our problem.

- WTWY Annual Gala Date:  	Saturday, July 1, 2018.  
- Gala Location:  			Flatiron District (Tech Hub)
- WTWY Street Teams:		Four teams, two shifts a week
- Source Data:				MTA Turnstile Data

**Data Cleaning**
Given the parameters above, we decided it would be best to look at all data from May and June from 2015 through 2017.  Once we read the data into python our team quickly realized that there was a bit of work to do before we could begin our analysis.  As a group we started to sieve through the dataset noting down causes for concern.  A few issues that were raised were: turnstiles which were counting backwards, turnstiles with counts which were being reset, varying time intervals, different subway station names for the same station, and varying subway line orderings.  

**Data Analysis - First Pass**
After cleaning up these data points we moved on to data analysis.  The first thing we were concerned with was sorting stations by total traffic (total traffic being defined as people entering + people exiting).  As you can see in the graph below we got many of the transit hubs that one would expect to see.  Once we saw this we deliberated on how we wanted to further filter the data since many of these highly trafficked stations were also extremely large, containing several different entries and exits, making it difficult for a canvasser to effectively target those who are passing in and out of station.  By looking at average subway traffic on a turnstile basis rather than on a total station basis we were able to get a better sense for the highest traffic subway entrances.  Once we put together this analysis we were looking at the second graph below.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/top_10_total_passengers.png)

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/top_10_times_subway_traffic_density.png)


**Data Analysis - Second Pass**

Additionally, we knew that many of the people passing through these stations would be working in a diverse set of industries as they head to and from work, and so we also wanted to decrease the search area to primarily the tech hubs of NYC. Using a list of top tech employers in NYC and focusing on employers who have 400+ employees, the team put together the following map which shows a density of tech employers between 14th and 34th street. As a result our final step was to limit our search to subway stations between these two cross streets, resulting in our final results displayed below:

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/top_10_revised.png)

To further demonstrate our point on why we want to look at average turnstile traffic versus average station traffic consider the following example.  The Penn Station subway stop, while it might be the most trafficked subway stop in all of NYC, contains 24 street entrances between 31st street and 34th street between 7th and 8th avenues.  Additionally there is significant turnstile traffic from passengers of the NJ Transit and Amtrak who rarely even come above ground before heading on their way to their final destination.  Compare this to the traffic at a station like 23rd street and 6th avenue, which only has 4 entrances all of which are located on the same block, while the station has significantly less traffic, all of the traffic is being released through these four stations providing a better location for a canvasser. By controlling for the number of turnstiles and looking for average turnstile traffice, we are able to best 