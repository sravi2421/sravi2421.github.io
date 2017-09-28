---
layout: post    
title: The Times Over Time
---

*A Look at New York Times Content from 1981 to 2016* 

Following the most recent presidential election, I started to look at the news with a much more critical eye than ever before. How could it be that Trump took the Presidency with such a convincing victory when most  news sources told us that this election was out of reach. I remember distinctly listening to a NYTimes Podcast in the days leading up to the election where  their closing question was whether the election result was going to be a landslide in Hillary's favor.  It was a clear case of the media telling their audience what they wanted to hear rather than providing the disciplined reporting which news organizations pride themselves on.  

With these set of events as inspiration, I set out to look at the NYTimes articles over the last 35 years and see what our country was focused on throughout this time period. My goal was to get a sense for what major topics dominated the news cycle during each time period. I also wanted to see whether or not there has been added component of sensationalism in the news in recent years when compared to the news of a few decades ago.  To look at that, I examined how descriptive language has changed over time.

**The Data**

Using the New York Times API I was able to get a hold of a summary of all articles by the New York Times for any given year. The API returned only the leading paragraph, headline, and snippet from each article, but also provided a url.  Using the urls provided and scrapy I scraped all front page news articles. The decision to pull only front page articles was made to capture what on the front of people's minds throughout each time period as opposed to an exhaustive list.  With this in place I now had the full text of approximately 300,000 front page articles published between 1981 and 2016.

**Topic Modeling**

Since I was interested in looking at how language and topics changed over time, I had to segment articles into time periods for analysis. As I looked at the first few topic models I ran, I saw that there was a natural topic which crept up around elections, and decided to use election cycles as the break point. So from here on out, each model which was created was created for nine time periods of four years each - (1981-1984, 1985-1988....2013-2016).

From there I used tf-idf vectorizer in conjunction with both NMF and LDA to provide clusters. After looking at a few different configurations, I found that the five category NMF model yielded the best results. Business and politics were consistently extracted as a cluster for every time period, with other clusters such as entertainment, sports and culture regularly showing up as well. Other more specific clusters tended to show up even with the five topic model, such as Russia, Foreign Relations, and local politics.  With these topic models in place, I wanted to drill down and get a bit more granularity and look at subtopics. To do so, I repeated the process using only the articles classified as Business and Politics respectively.

**Subtopics - Politics**

For politics, once again the NMF model with five subtopics provided the optimal separation. Within the Politics topic, the most common subtopics were: The Middle East, Presidential Campaigns and Judicial Issues. Looking at article counts over time, you can see how the country's attention span changed over time.  Below are a few observations I took away by looking at the stacked bar chart below.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/Article_counts_over_time_politics.png)

- Military conflicts dominate news coverage. Throughout the 1980s you can see Russia as a major topic which tapers off after the end of the Cold War.  Throughout the 2000's, the Middle East and Terrorism are the two largest subtopics, even removing the Presidential Election as a subtopic from 2005 to 2008.
- The Lewinsky Scandal displaced traditional domestic news. From 1997 to 2000, the Lewinsky Scandal managed to displace the subtopics 'Domestic Affairs' and even dampened the country's attention towards the Middle East.
- Domestic affairs have taken a backseat in recent times.  Looking at the subtopics Judicial Issues, and Domestic, which cover court cases and domestic legislation, both have received smaller article counts as compared to foreign affairs issues over the past 10 to 15 years.  

Lastly with this crazy election that we just had I looked specifically at the Presidential Election Topic to see if there were any interesting trends. One interesting thing which the topic modeling showed was that there were two distinct 'Presidential Election' topics for the 2016 election, something which did not show up in any other year. In total, there were close to the same number of articles published for this election cycle as several others before this. This seems to indicate that there were clear distinctions in the way that the NY Times covered the Republican and Democratic races which was quite different than the several elections leading up to this one.

**Subtopics - Business**

When going through the business subtopics, I quickly realized that the ocean of topics in the corporate world was larger than what I had seen in Politics and after trying a few different models, I found that specifying eight topics extracted the best results. Topics which were extremely prevalent throughout the entire analysis included 'Corporate' which was a pretty broad category centered around corporate earnings of all types of corporations, after that, economic indicators, oil, stocks and banking were pretty prevalent throughout the entire analysis.  The only industries which were extracted as their own subtopic were the Tech, Motor, Healthcare and Retail industries.  The Motor Industry was a topic throughout the analysis with Technology only becoming prevalent in the early 1990s.  Healthcare and Retail were less prevalent throughout the analysis and were only subtopics between 2005 and 2016.

![test](https://github.com/sravi2421/sravi2421.github.io/raw/master/images/Article_counts_over_time_business.png)

**Word2Vec Sentiment Analysis**

After extracting subtopics, I was curious to see how the Times modified their description of key topics throughout time. To examine word descriptions I used Word2Vec, a model used to extract Word Embeddings from corpuses of text.  Since I wanted to specifically look at descriptors, I went through and tagged each adjective or adverb within my body of text using a part of speech tagger prior to creating my Word2Vec models.  With this done, I created separate Word2Vec Models on the subtopics of the Middle East and Domestic Affairs.  Using those I extracted the primary words associated with Moscow, for the Middle East corpus and President for the Domestic Affairs corpus as shown below.

***President, 1981-1984(Reagan)***

<img src="https://github.com/sravi2421/sravi2421.github.io/raw/master/images/reagan_1981_1984.png" alt="Drawing" style="width: 350px;"/>

***President, 2009-2012(Obama)***

<img src="https://github.com/sravi2421/sravi2421.github.io/raw/master/images/president_2009_2012.png" alt="Drawing" style="width: 350px;"/>

These are two interesting characterizations of the President at different times during the history of our country. You can see that both presidents were described in positive terms and were seen as unifying.  But when looking at a few of the medium sized words (size is in direct relation to frequency), you can see that Reagan was characterized as a plain spoken politician who was relatable, with descriptors such as 'mainstream', 'bluntly', and 'plainly'.  Whereas Obama was seen in a more timid intellectual fashion, with descriptors such as 'philosophical', 'nervous', 'polite', and 'conciliatory'.  Interestingly both of them were described with both positive and negative descriptors. For Reagan these descriptors included 'futile' and 'combative' whereas for Obama, these words included 'negative'and 'forcefully'

***Moscow, 1981-1984***

<img src="https://github.com/sravi2421/sravi2421.github.io/raw/master/images/moscow_1981_1984.png" alt="Drawing" style="width: 350px;"/>

***Moscow, 2013-2016***

<img src="https://github.com/sravi2421/sravi2421.github.io/raw/master/images/moscow_2013_2016.png" alt="Drawing" style="width: 350px;"/>

Interestingly, for Moscow, the descriptors used during the early 1980s are less emotionally charged than those from 2013 through 2016, despite the fact that the United States was engaged in the cold war at that time.  For example, several of the top descriptors during the cold war period include 'openly', 'likely', 'cool' and 'deeply'.  Whereas from 2013 to 2016, the largest words include 'brokered', 'intrusive', and 'abrupt'.
