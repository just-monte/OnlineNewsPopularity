![cover photo](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%206.46.35%20PM.png)
# Online News Popularity
[Mashable](https://mashable.com) is an online news distributor. The company operates and maintains an online platform, with a focus on topics such as technology and social media. Mashable is interested in knowing what influences their number of shares to increase their popularity.
## 1. Data 
The dataset was obtained from the UCI Machine Learning Repository. The dataset summarizes a heterogeneous set of features about articles published by Mashable over 2 years (01/07/2013 to 12-27-2014). To view the dataset click on the link below: 
> * [UC Dataset](http://archive.ics.uci.edu/dataset/332/online+news+popularity)
## 2. Data Wrangling 
[Data Wrangling](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Data%20Wrangling.ipynb)

The original dataset was composed of 61 columns and 39644 rows. The majority of column items were floats with the expectation of column “URL” which are objects, and “shares”which are integers. The dataset was clean. Upon checking, the dataset was missing the articles’ published date. This is a useful piece of information as it can show seasonal trends if any. To obtain the articles' published date, I web scraped from each article. I was able to do this by creating a loop that extracted the data from each article using the URLs in the dataset. After each date was obtained, I checked the column for any null values in which no null values were found. The finalized dataframe is composed of 62 columns and 39644 rows.
## 3. E.D.A.
[E.D.A.](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/EDA%20.ipynb)


The heatmap showed correlations between: kw_max_avg and kw_avg_min, avg_negative_polarity and min_negative_polarity,  abs_title_sentiment_polarity and title subjectively,  self_refernece_avg_shares and kw_avg_avg, data_channel_is_worlds and LDA_02, data_channel_is_bus and LDA_00

Article shares mean was 3395.380 with the median being 1400.00. The max article share was 843300. 

![](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%207.30.55%20PM.png)

The articles were divided into 2 categories: popular and unpopular. The articles were placed on whether or not the article’s share reached the mean. Out of the days of the week, Tuesday and Wednesday had the highest count of unpopular articles with a count reaching 6,000 each. Monday, Tuesday, Wednesday, and Thursday all tied in popular articles reaching over 1000. The article channels were lifestyle, entertainment, business, social media, tech, and world. World articles came in first in unpopular articles reaching over 7000. Tech was first in popular articles with over 1000 articles. Number of words per content, number of images and videos share the same relationship. The lower number of words. Images and or videos led to higher article shares.  Higher shares were seen between articles whose titles were between 8 and 13 words.

![](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%207.50.35%20PM.png)

LDA_02 had the highest count of unpopular articles with over 7000 articles. LDA_03 has the highest count of popular articles reaching over 2000 articles. Surprisingly, all tiers of LDA have counts of popular articles 1000 and over.


## 4. Algorithms & Modeling 
[Modeling](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Pre-processing%20%26%20Modeling.ipynb)

The data was split using a time series split  on the date September 1, 2014. All dates before September 1, 2014 were used for training, and the dates after were used for testing. 
![](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%208.59.14%20PM.png)

After cross-validation, I created the time series features for the model. The features being  day, month, year, and day of week. The model I chose was XGBoost. The number of trees was set to 500 estimators with a learning rate of 0.01. The model was fit to the train and testing data with verbose to 50 to avoid overfitting. I did notice some overfitting around the 200 mark. I evaluated the model using the mean squared error. The model scored 8071.733668467614.

The worst predicted days were 8-22-2014, 08-31-2014, 10-04-2014, 09-25-2015, 9-19-2015. The best predicted days were 11-28-2014, 09-07-2014, 11-15-2014, 09-21-2014.
## 5. Model Predictions 
Based on the month, month was highest in importance with a score of 0.38. Day is second with 0.23, day of week third with 0.20. Year was ranked lowest in importance with 0.19.
![](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%208.59.24%20PM.png)

## 6. Forecating 

Higher peaks were noted at the beginning of the year( January - May).The highest shares appeared in March 2015 with over 5500 shares.Mid May one can see the shares decrease in which articles shares all fall under 3000 (June-December). The lowest shares appeared in November 2015 with under 2500 shares.

![](https://github.com/just-monte/OnlineNewsPopularity/blob/c0c707a90dd62027051944a2b29b88b771f206e4/Images/Screenshot%202023-08-16%20at%208.59.36%20PM.png)

## 7. Future Improvements 
To improve on this model, I would add additional features such as quarter, and holidays. It would have been helpful insight if the times the articles were published where available. This would have allowed for another depth in the seasonal trends.  Lastly would take into account lagged features. 
