---
layout: post    
title: The Times Over Time
---

*A Look at New York Times Content from 1981 to 2016* 

After our most recent presidential election, I started to look at the news with a much more critical eye than ever before. How could it be that Trump took the Presidency with such ease when most of our news sources told us that this election was out of reach. I remember distinctly listening to a NYTimes Podcast and their closing question they posed was whether the election result was going to be a landslide, in Hillary's favor.  It was a clear case of the media telling their audience what they wanted to hear rather than providing disciplined reporting which new organizations pride themselves for.  

With these set of events as inspiration, I set out to look at the NYTimes articles over the last 35 and see what our country was focused on throughout this time period. My goal was to get a sense for what major topics dominated the news during each time period as well as see how descriptive language has changed over time.

**The Data**

Using the New York Times API I was able to get a hold of a summary of all articles by the New York Times for any given year. The API returned only the leading paragraph, headline, and snippet from each article, but also provided a url.  Using the URL's provided and scrapy I scraped all front page news articles. The decision to pull only front page articles was made to capture what on the front of people's minds throughout each time period as opposed to an exhaustive list.  With this in place I now had the full text of approximately 300,000 front page articles published between 1981 and 2016.

**Topic Modeling**

Since I was interested in looking at how language and topics changed over time, I had to segment articles into time periods for analysis. As I looked at the first few topic models I ran, I saw that there was a natural topic which crept up around elections, and decided to use election cycles as the break point. So from here on out, each model which was created was created for nine time periods of four years each - (1981-1984, 1985-1988....2013-2016).

From there I used tf-idf vectorizer in conjunction with both NMF and LDA to provide clusters. After looking at a few different configurations, I found that the five category NMF model yielded the best results. Business and politics were consistently extracted as a cluster for every time period, with other clusters such as entertainment, sports and culture regularly showing up as well. Other more specific clusters tended to show up even with the five topic model, such as Russia, Foreign Relations, and local politics.  With these topic models in place, I wanted to drill down and get a bit more granularity and look at subtopics. To do so, I repeated the process using only the articles classified as Business and Politics respectively.

**Subtopics - Politics**

For politics, once again the NMF model with five subtopics provided the optimal separation. Within the Politics topic, the most common topics were: The Middle East, Presidential Campaigns and Judicial Issues. Looking at article counts over time, you can see how the country's attention span changed over time.  Below are a few observations I took away by looking at the stacked bar chart below.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/Article_counts_over_time_politics.png)

- Military conflicts dominate news coverage. Throughout the 1980s you can see Russia as a major topic which tapers off after the end of the Cold War.  Throughout the 2000's, the Middle East and Terrorism are the two largest subtopics, even removing the Presidential Election as a subtopic from 2005 to 2008.
- The Lewinsky Scandal displaced traditional domestic news. From 1997 to 2000, the Lewinsky Scandal managed to displace traditional domestic news and dampened the country's attention towards the Middle East.
- Domestic affairs have taken a backseat in recent times.  Looking at the subtopics Judicial Issues, and Domestic, which cover court cases and domestic legislation, both have received tapered article counts as compared to foreign affairs issues.  

Lastly with this crazy election that we just had I looked specifically at the Presidential Election Topic to see if there were any interesting trends.  In total, it looks as though the most recent election received just as much coverage as elections in the past, with the most comparable one being the Bush/Gore election which had a fair bit of controversy surrounding it as a result of the vote recount in Florida. One interesting thing which the topic modeling showed was that there were two distinct 'Presidential Election' topics for the 2016 election, something which did not show up in any other year. This seems to indicate that while the total coverage for the campaigns was not that different from before, there were clear distinctions in the way that the NY Times covered the Republican and Democratic races which was quite different than before.

**Subtopics - Business**

When going through the business subtopics, I quickly realized that the ocean of topics in the corporate world was larger than what I had seen in Politics and after trying a few different models, I found that specifying eight topics extracted the best results. Topics which were extremely prevalent throughout the entire analysis included 'Corporate' which was a pretty broad category centered around corporate earnings of all types of corporations, after that, economic indicators, oil, stocks and banking were pretty prevalent throughout the entire analysis.  The only industries which were extracted as their own subtopic were the Tech, Motor, Healthcare and Retail industries.  The Motor Industry was a topic throughout the analysis with Technology only becoming prevalent in the early 1990s.  Healthcare and Retail were less prevalent throughout the analysis and were only subtopics between 2005 and 2016.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/Article_counts_over_time_business.png)

**Word2Vec Sentiment Analysis**

After extracting subtopics, I was curious to see how the Times modified their description of key topics throughout time. To examine word descriptions I used Word2Vec, a model used to extract Word Embeddings from corpuses of text.  Since I wanted to specifically look at descriptors, I went through and tagged each adjective or adverb within my body of text using a part of speech tagger prior to creating my Word2Vec models.  With this done, I created three separate Word2Vec Models on the subtopics of the Middle East and Domestic Affairs.  Using those I extracted the primary words associated with Moscow, for the Middle East corpus and President for the Domestic Affairs corpus as shown below.

***President, 1981-1984(Reagan)***
![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/reagan_1981_1984.png)

***President, 2009-2012(Obama)***
![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/president_2009_2012.png)


***Moscow, 1981-1984***
![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/moscow_1981_1984.png =100x20)

***Moscow, 2013-2016***
![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/moscow_2013_2016.png)




