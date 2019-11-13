# Using Social Media to Predict Power Outages
###_Authors_: Peter Garcia, Raffy Santayana, Ambar Kleinbort
---

## Problem Statement
The aftermath of Hurricane Sandy led to over [8 million US people without power](https://www.huffpost.com/entry/hurricane-sandy-power-outage-map-infographic_n_2044411). According to [energy.gov](https://www.energy.gov/articles/hurricane-sandy-noreaster-situation-reports), everyone who was able to recieve electricity after the storm has had their electricity restored by December 3, leaving a remainder of 26,000 people in New York and New Jersey without power. One of the methods of detecting power outages at this time was by utilizing [smart meters and Advanced Meter Infrastructures (AMI)](https://openei.org/wiki/Definition:Outage_Detection/Reporting). The problem is that these systems [will not be fully implemented until 2030](http://people.stern.nyu.edu/kbauman/research/papers/2015_KBauman_WITS.pdf) due to high cost of production. As an alternative method of detecting these outages, we will be using natural language processsing techniques such as web embedding to analyze various posts from a social media platform, Twitter. When analyzing these posts, we hope to classify each post as either a post pertaining to a blackout or a post not pertaining to a blackout using supervised classification.

## Project Files
1. [Scraping Twitter for Tweets](https://github.com/PeterGarcia95/DisasterRelief/blob/master/code/01%20-%20Scraping%20Twitter%20for%20Data.ipynb)
2. [Identifying Known Blackouts in Mass](https://github.com/PeterGarcia95/DisasterRelief/blob/master/code/01-Identifying%20Known%20Blackouts%20in%20Mass.ipynb)
3. [Tweet Cleaning](https://github.com/PeterGarcia95/DisasterRelief/blob/master/code/02-Tweet%20Cleaning.ipynb)
4. [NLP and Model Evaluation](https://github.com/PeterGarcia95/DisasterRelief/blob/master/code/03-NLP%20and%20Model%20Evaluation.ipynb)
5. [Mapping Boston Tweets](https://github.com/PeterGarcia95/DisasterRelief/blob/master/code/04-%20Mapping%20Boston%20Tweets%20.ipynb)

## Executive Summary
In order to get Tweets from Twitter to perform natural language processing analysis, we will be utilizing a Python library called [twitterscraper](https://github.com/taspinar/twitterscraper). With this library, we are able to establish keywords to search for that we expect to be within the text of the Tweet, keywords we do not want within the text of the Tweet, the general area we would like the origin of the Tweets to be, and the range of distance we would like to limit the Tweets to be from. Due to the large amount of Tweets posted within the USA, we will be limiting our Tweets to originate from the center of Boston, MA within a radius of 75 kilometers.

Once the Twitter data is gathered, we will use [data from the Department of Energy](https://www.oe.netl.doe.gov/OE417_annual_summary.aspx) to determine which Tweets were posted during actual blackouts. This way, we are able to use supervised classification models such as logistic regression and k-Nearest Neighbors. Since we are limiting our Tweets to originate from the general Boston area, we are also able to determine which blackouts affected Massachusets.

With all the labeled Tweets in hand, we are then able to clean the text of the Tweets by removing superficial tokens that may come from HTML links or otherwise to then be able to apply `CountVectorizer` to get the frequency of each token in their respective document, or Tweet. Thus, we will pipeline and GridSearch in order to tune hyperparameters. We will then look at various evaluation metrics such as the ROC AUC.

## Conclusions, Recommendations, and Limitations
**Explain Why We Used Logistic Regression and CountVectorizer For Final Results**

**Discuss the Evaluation Metrics Used and ROC AUC**

Since the the Twitter data was scraped using a third party Python library and not the Twitter API, we were unnable to get reliable geolocation information, if any. Due to this, we needed to populate simulated location values for each Tweet. When visualizing the location of Tweets that were posted during blackouts and those that were not, we expect to see clusters of neighborhoods that were affected, but did not occur due to the randomly assigned location values.

Adding on to the lack of reliable location data, we were not able to be completely certain that the Tweets we have gathered truly originated from Massachussets. For example, while querying for Tweets, we needed to specify to not scrape Tweets that originated from or mentioned @KenyaPower_Care. Obviously, those in Massachusets do not recieve energy from Kenya, but it is apparent that twitterscraper's query function is not perfect when using the `near` and `within` parameters.
