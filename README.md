
# @RealScientists Preliminary Analyses  

The preliminary analyses are to get a better understanding of the data. Some important things to keep in mind: although this dataset is rich, more supplemental data is necessary to truly paint a better picture. Most of the preliminary analyses presented here are primarily based off of the Twitter data and the blog post introduction questionnaire. Although these analyses are presented as what I would consider exploratory analyses, there is a strong need for someone to truly take much care in joining metadata post-hoc to the current dataset. Other recommendations are presented throughout.  

The major recommendations:
* Better cleaning of the current data and metadata (introduction questionnaire, pre-follower data, post-follower data) in order to accurately assess the naturalistic phenomena associated with the account. This would most likely be best provided by some sort of data-specific internship.  
* A larger understanding of the text data. Basic naturalistic language processing has been insightful, but more is absolutely necessarily based on some of the preliminary analyses which are limited and would be better assessed via NLP or different text-based analytics.  
* Supplementing the end of the week with more moderator-led chat or engagement activities. There is a consistent observation of Friday and Saturday being relative low-points of engagement. In terms of growing the account (or efficiently using all of the days in a week), maintaining or increasing engagement towards the end of the week should be a strong priority in the future.  

## Initial Descriptions  
### Data  
Before jumping into the analyses, I would like to briefly explain the data. The data from analytics.twitter.com tracks data from tweets. However, some columns of data are not intuitive. For example, take _follows_. Anecdotally, there is always far more follows per day than recorded by the data. Why? Because the data tracks information from within a tweet. Follows within one tweet will be far less than follows after someone first clicks on the user profile name and then reads multiple tweets. This leads to a follow from the profile page (not any specific tweet) and therefore does not get included in the dataset.  

Here is what follows look like across a week:  
!['Follows'](../master/viz/prelim01_01.png)  
Here is what user profile clicks look like:  
!['User profile clicks'](../master/viz/prelim01_02.png)  

I know that, on average, there are far more than 20 follows per week and far less than 2000 follows per week (anecdotally). If we pretend that 5% of user profile clicks end up being follows, then ~100 follows per week sounds a little more accurate.  

As you may have noticed, the data does not track any "loss" data -- or rather, unfollows (or unlikes, unretweets, deleted replies, blocks/mutes). 

### Impressions, Engagements, and Views  
Two aggregate statistics are provided by Twitter: impressions and engagements. They are defined by Twitter as:  
> **Impressions**: The number of times a user saw a Tweet on Twitter  
> **Engagements**: Total number of times a user has interacted with a Tweet. This includes all clicks anywhere on the Tweet (including hashtags, links, avatar, username, and Tweet expansion), retweets, replies, follows, and likes.  

These statistics can be (somewhat) easily recreated using the raw data provided by analytics.twitter.com. We can visualize impressions and engagements over the week on @realscientists:  
!['Impressions'](../master/viz/prelim01_03.png)  
!['Engagements'](../master/viz/prelim01_04.png)  

A few things are very noticeable here. Impressions are greater than engagements by a couple orders of magnitude. Impressions themselves follow a somewhat predictable trajectory, with greater impressions earlier in the week and slowly decaying as the week continues. The engagements are less predictable, with Thursday and Saturday being largely more variable than other days. One issue with impressions and engagements is that engagements are apart of impressions. Or, in other words, in order to create an engagement, someone must also create an impression. If you simply subtract engagements from impressions, the difference is views without engagements.  
!['Views'](../master/viz/prelim01_05.png)  

Views are similar to impressions (the magnitude of values are the same) so it is difficult to see the differences here. But there is an issue with presenting data in this way. Raw "counting" data (i.e. things you can add together, like retweets) might be poor representation when one curator is perhaps less popular than another -- or perhaps one curator tweets less than another. In either of these cases, counting data would punish those with fewer counts. However, there is precedent for infrequent tweets and many engagements (see: celebrity tweets) and also frequent tweets with very few engagements (see: new Twitter users). A perhaps more "fair" way to assess these differences would be to use rate statistics.  
!['View rate'](../master/viz/prelim01_06.png)  
!['Engagement rate'](../master/viz/prelim01_07.png)  

View rate (or "view_rate") is views divided by impressions. In contrast, engagement rate (or "engagement_rate") is engagements divided by impressions. In the majority of cases, the object is to predict engagements since engagements are more equivalent to maintaining an active audience than views. To further see the relationship between engagements and views, we can simply demonstrate a ratio between the two:  
!['Engagement ratio'](../master/viz/prelim01_08.png)  

Engagement ratio and engagement rate are similar, but the denomenators are very different. Some statistics will be shown as rate and some as ratio. Currently, there's no standardization to which is a better source of data for either descriptive or predictive statistics. Here's a description of these statistics:  

stat | impressions | 	engagements | 	views | 	view_rate | 	engagement_rate | 	engagement_ratio
--- | --- | --- | --- | --- | --- | --- 
count | 	6.940000e+02 | 	694.000000 | 	6.940000e+02 | 	694.000000 | 	694.000000 | 	694.000000
mean | 	1.641592e+05 | 	3083.821326 | 	1.610754e+05 | 	0.981092 | 	0.018908 | 	0.019393
std | 	1.491498e+05 | 	4105.857814 | 	1.458605e+05 | 	0.010550 | 	0.010550 | 	0.011218
min | 	2.280000e+02 | 	6.000000 | 	2.090000e+02 | 	0.899202 | 	0.003289 | 	0.003300
25% | 	5.900025e+04 | 	1006.500000 | 	5.768025e+04 | 	0.977600 | 	0.011641 | 	0.011778
50% | 	1.279550e+05 | 	2007.000000 | 	1.247725e+05 | 	0.983215 | 	0.016785 | 	0.017071
75% | 	2.119950e+05 | 	3772.500000 | 	2.096872e+05 | 	0.988359 | 	0.022400 | 	0.022913
max | 	1.370753e+06 | 	56473.000000 | 	1.314280e+06 | 	0.996711 | 	0.100798 | 	0.112097  

The primary goal when working with this current dataset is to describe what makes a person engage at a high rate. Ideally, high engagement correlates with account growth. If there are particular curators who are efficient in engagement rate then ideally it may be possible to predict who those types of people are and be more specific when structuring how to schedule curators for the account.  

As the data analyses unfold below, keep in mind that engagement rate should be somewhere between 1.5% and 2.0% on average, with a liberal range of 1% to 3%. 

## Group data  
One aspect of describing how people engage is if there are particular groups of curators who engage more effectively than others. Some of the groups presented here are logical and intuitive to understand whereas other groups may be less intuitive.  

For example, engagement rate increases as a curator creates more media views.  
!['Media views'](../master/viz/prelim01_09.png)  

This is fairly intuitive -- more media (like images or video) creates more engagements than less media. Other graphs seem intuitive, like this graph on popular word usage:  
!['Popular words (engagements)'](../master/viz/prelim01_10.png)  

However, when converted to engagement rate, this finding is nearly in a null-to-opposite direction:  
!['Popular words (engagement rate)'](../master/viz/prelim01_11.png)  

Intuitively, you would assume using the top 50 words that created the most retweets would have greater engagements than any other words (and that is partially true in the engagement counting statistic). However, since engagement rate is more accurate when comparing efficiency of engagement, there tends to be less engagement efficiency when using popular words. This seems less intuitive, but the logic still follows: the "lurker" who tends to read something but selects not to interact with a tweet is greater than an active engager (and that was true from the original analysis, showing ~1.8% engagement rate). However, as the counts increase for engagements, it's possible that the views increase in a non-linear, perhaps exponential manner. Or, more statistically speaking, the relationship is not:    

![eq1](http://latex.codecogs.com/gif.latex?%5Ctext%7BEngagement%20rate%7D%20%3D%20%5Cfrac%7B%5Ctext%7BEngagements%7D%7D%7B%5Ctext%7BImpressions%7D%7D)

But perhaps the actual rate of engagement is more like:  

![eq2](http://latex.codecogs.com/gif.latex?%5Ctext%7BEngagement%20rate%7D%20%3D%20%5Cfrac%7B%5Ctext%7BEngagements%7D%7D%7B%5Ctext%7BImpressions%7D%5EX%7D) 

Where $X$ is some sort of growth factor. Needless to say, the complexity between engagements and impressions is perhaps greater than the simple analytics presented here.  

In one more grouping analysis, the difference between different branches of science seem to be less clear. Below is both engagements and engagement rate:  
!['Branches of science (engagements)'](../master/viz/prelim01_13.png)  
!['Branches of science (engagement rate)'](../master/viz/prelim01_14.png)  

This is a particular area where rate statistics are more clear than counting statistics. In this particular analysis, there is an unbalanced pool of people from these branches of science. 

Science | Curators (multiple fields possible)
--- | ---
astro |19
geo | 28
socio | 5
psych | 15
bio | 84
chem | 48
physics | 38
 | _Note: Most likely inaccurate_  
 
For example, on Sunday, socio- fields look underrepresented in engagement counting stats, but engagement rate makes socio- look more typical. In contrast, astro- fields looks only slightly better in engagement counting stats than other fields but the engagement rate demonstrates how astro- fields tend to be significantly better at engagements on Sundays than other fields.  

Branches of science itself is a particularly interesting grouping metric since there is a possible hypothesis that certain sciences are more popular than others. However, in a demonstration of machine learning (presented in detail in the machine learning section), all branches of science did not have a positive coefficient for predicting engagement rate. This suggests that even though there are significantly different engagements per day during the week, the ability to predict a significantly different trend simply due to a branch of science is not possible currently.  

There are other reasons to group data that are not solely for grouping due to describe trends in data. It is possible to leverage grouping using unsupervised methods (like K-means clustering) in order to identify outliers with objectivity. Take for example engagement rate as a function of views:  
!['Engagement groups (quantiles)'](../master/viz/prelim01_15.png)  
!['Engagement groups (KMeans)'](../master/viz/prelim01_16.png)  

Groups in the first graph are divided into high engagement rate ('hi'), medium engagement rate ('md'), and low engagement rate ('lo'). These groups are divided by the top 95% of engagements ('hi'), engagements between 5% and 95% ('md'), and the bottom 5% of engagements ('lo'). The issue with this rigid grouping is how much data would be eliminated if high engagement was rejected as "outlier" and how little information is removed when low engagement is treated as "outlier". The second graph uses K-means clustering instead of quantiles. The KMeans clusters data in three ways: first, those with low views but high engagement; second, those with "proportional" views and engagements; and lastly, those with low engagements but high views. There still tends to be much data to remove in the low-view-high-engagement cluster, but this is less rigid and more objective than subjectively rejecting data simply because the data seems like an outlier. 

## Machine Learning Techniques
A possible route is leveraging machine learning methods to describe and predict engagements. K-means presented above is one avenue of machine learning that may be advantageous. Another is simple machine learning models. Also described briefly in grouping, we trained a linear model to predict engagement rate using each branch of science, the day, the time of day (in hours), and the curator's personal account name. 

Feature | Beta | p-value
--- | --- | ---
socio |           0.001011 | 0.290
astro |           0.000723 | 0.087
**day** |         **0.000326** | **<0.001**
psych |           0.000301 | 0.708
**handle** |    **-0.000045** | **<0.001**
**hour** |           **-0.000062** | **<0.001**
geo |            -0.000068 | 0.849
physics |        -0.000419 | 0.198
**bio** |            **-0.000929** | **<0.001**
**chem** |           **-0.001777** | **<0.001**
**Bold**: _p_<0.05 | | 

Although some of these values are reported as significant, this is a bit misleading. Handle, hour, and day are all magnitudes less than the most meaningful unit (this is a rate statistic, so roughly 0.005 and greater would be meaningful). Bio- and chem- fields are also significant but significance is 5x greater than the reported beta coefficient. In all of these weights, there is no significant predictor for engagement rate. Day and hour is seemingly striking. You might assume tweets in specific hours of the day would be engaged with more often than others (i.e. in West Europe or Eastern US waking times), but this is simply not the case. Also with day, there is a demonstrated decay of engagement as the week goes on, but day was not a significant predictor of engagement rate. It is possible that engagement decay is also logarithmic or polynomial function and a linear model is inadequate. This is also true for each feature in this model. Other machine learning methods, like random forests after a polynomial fit, might be better to implement.  

When trying to fit the above features to a predictive linear model:  
!['Engagement rate prediction'](../master/viz/prelim01_17.png)  

The correlation of predicted values (x-axis) on real values (y-axis) is extremely weak. This was already known from the weak beta coefficients, but visually it does beg the question of whether some sort of grouping factor (like the one presented with KMeans) may be actually advantageous for prediction over features like hour, day, or branch of science. 

### Natural Language Processing  
Branches of science was a basic text mining exploration that would roughly fall under natural language processing. The extraction of popular words (mentioned in the grouping section) was also a natural language processing analysis. From the popular words analysis, the following list of words were extracted as the top words used in the most retweeted tweets:  

Words |  |  |  |  |  | 
--- | --- | --- | --- | --- | --- 
https | 	twisteddoodles | 	awesome | 	scientific | 	new | 	reading
http | 	times | 	tufts | 	follow | 	order | 	really
science | 	authorship | 	sun | 	kit | 	twitter | 	reason
use | 	time | 	station | 	young | 	paper | 	rt
realscientists | 	today | 	share | 	hydrogen | 	ear | 	woman
talk | 	scientist | 	selected | 	life | 	ppl | 	antarctica
amp | 	things | 	come | 	living | 	publishing | 	years
answer | 	best | 	thread | 	happy | 	did | 	academia 
great | 	tap | 	leave | 	h20 | 	determining | 	work  

It seems as though grouping and modeling methods are limited without truly diving into the contents of the text data. More complex models could perhaps help, but the text data is rich and relatively untapped. On top of this, more clean data would also help -- like making sure the curator weeks are accurate to the handle names, or that the curator's branch of science is labeled correctly.

## Preliminary Conclusions  
There is still much to do, but the most informational analyses seem to be:  
* There seems to be less engagement towards the end of the week that should be capitalized on by supplementing the account with other engagement campaigns  
* Different grouping is necessary to have a larger understanding of what generates graeter engagement  
* Machine learning techniques may be better than subjective human reasoning for grouping or predictive methods  
* NLP and other text analysis methods should be the primary focus of analytics in the future  

### Recommendations
* More help with the data analyses. Currently, between me and seven other colleagues, the ~4 hours per week involved on this project is not enough to make large progress over the available data.  
* Someone helping with the data pipeline pre-analysis is seemingly essential. Joining dates, handles, and branches of science post-hoc will be very time consuming, albeit easy. This would be ripe for an internship. I personally have a contact in mind who would be very willing to do this work on a volunteer basis.  
* Adjustments to the current introduction questionnaire would help tremendously. 
    *Inclusion of a branch of science drop-down option, with a sub-field free response option is extremely recommended. 
    * A field for "curation start date" in order to accurately join data on date is also extremely recommended. 
    * The handle field being specific to only the Twitter handle without the @ sign is highly recommended. 
    * Follower count in only number values would be highly recommended (i.e. "10000" versus "10K"). 
    * Psychological-like questions are also recommended (i.e. "How nervous are you about tweeting?", "How excited are you about tweeting?", "On a scale, how much of your week is scheduled?", etc).  
    
These conclusions are preliminary so some (or many) of the current results are expected to change. However, most of the recommendations presented here are very important in terms of better data science. Lastly, if data science is to inform the @realscientists account on (ultimately) best recommendations for growth, then the current recommendations should be implemented as soon as possible (in my own personal recommendation, the questionnaire adjustments before the end of the year; interns and other volunteers by January). 
