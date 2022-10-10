# NLP_Sentiment-Analysis-of-Reviews-in-Steam
Analyze relationship between toxicity level of reviews and gaming time with Steam API. Built fake review detection mechanism using feature selection&amp; scaling, K-means clustering and KNN model. (This is a group project)

## Problem statement:
1. As the video games are gainining popularity worldwide, especially in the context of Covid-19, gaming communities have become very active. Game reviews on distribution platforms such as Steam, GamersGate, and Discord Store is one of the main approaches for users to express their attitudes.
2. Among these game reviews, there is problematic and toxic content which is hindering development of the gaming industries and effective communication among game players.
3. Therefore, as the gaming industies grow and more people are joining gaming communities, it is important to understand players' attitudes and the severtity of toxic content in game reviews.

## Data Collection & Processing
1. Steam API: get review (40,000 + reviews)
2. Perspective API: measure toxicity of reviews (10,000 reviews due to rate limit)

We used "Steamworks Web API", which is an official API, to acquire user reviews of games, game statistics, user statistics and Steam community data. 
And we retrive data from *Dota 2* as our main source for this analysis. 


## RQ1: Did user sentiment changed positively, negatively, or stayed relatively similar compared to pre-pandemic?
### - Visualization of Sentiments over Time
(The reviews range from August 2011 to May 2022, covering pre-pandemic periods.)

### - Define Time Periods

• Pre-pandemic: Before 2020 March

• Peaks of pandemic: 2020 March - 2021 June
### - Inference 
It seems that the sentiment scores measured by VADER decreased during the peak of pandemic. 

The toxicity level of reviews decreased during the peak of pandemic and returned to the level before pandemic since 2021 June.

### - Run t-tests to Check If Differences are Statistically Significant
### Interpretation 1
The difference of sentiment polarities between pre-pandemic and peak of pandemic is significant on the confidence level of 95%. That is to say, that there is a decrease in sentiment polarity during the peaks of pandemic. People had LESS POSITIVE sentiment during the peak of pandemic.
### Interpretation 2
The difference of sentiment polarities between peak of pandemic and post peak pandemic is significant on the confidence level of 99%. That is to say, that there is a decrease in sentiment polarity during and after the peaks of pandemic. People have LESS POSITIVE sentiment after the peak of pandemic.
### Interpretation 3
The toxicity level of reviews significantly decreased during the peak of pandemic. After the peak of pandemic, the toxicity level significantly increased and returned to the similar level of pre-pandemic period.

## RQ2: What is the relationship between toxicity level of reviews and user gaming time?
### Modeling gaming time and toxicity score
We would like to see whether game times will affect the attitude of players’ comment. From the scapped data, we are able to find several key measurements, such as play time forever and play time at review. In addition, we used the calculated toxicity score from the last assignment as our depedent variable. Our baseline model adopted ElasticNet regression and used the MAE(Mean Absolute Error) and MSE (Mean Sqaure Error) to access the performance, which are 0.173 and 0.230 respectively. The scores indicated the toxicity score could be measured by different gaming time variables.

## RQ3: What are typical linguistic patterns of fake reviews in the Steam Community?
### Fake Review Modeling
### Part I. Suspicious pattern clustering

Since there’s no general predefined criteria for “fake review”, we determine to perform 8 tasks that can identify suspicious patterns of fake reviews:
1. Find the total number of numbers
2. Find the length of review tokens (T)
3. Find the Ratio of total number of first-person words 4. Find the Ratio of total number of uppercase letters 5. Find the total number of punctuation symbols
6. Find the total number of short words
7. Find the ratio of total number of digits and symbols 8. Find extreme sentiment scores

After calculating suspicious pattern scores for each review, we decide to use unsupervised model, “K-means clustering to group similar reviews together.
In the process, we use elbow method to find the most optimal K, and we go with 20 clusters. ( Will explain why we use cluster=20 in below code block)
The cluster, namely our new variable, is treated as our conclusion on all fake review patterns above and can be used in later supervised-model analysis.

### Part II. Supervised model with manual labeling 

1. How we hand-label fake reviews: In order to detect fake review with supervised model, we hand-label 700 reviews using below criteria: - Ratio of digit in each review >=80% - The length of review tokens <=4 - Ratio of total number of first-person words >=1.8% - Ratio of total number of uppercase letters >=8.8% - Ratio of number of punctuation symbols >=17.89% - Ratio number of short words (less than 3 letters) >37.31% - Ratio of total number of digits and symbols >4.31%
After hand-labeling, 38.5% of all reviews are considered “fake” in 700 reviews.
2. Model selection: For fake review prediction, we decide to apply KNN model since our labeled dataset is small and with less features and noise. KNN model performs better with this condition. Our final model accuracy is arounf 74%

### Part III. Linguistic patterns based on model prediction

- Inference

1. Fake reviews have shorter length.
2. The ratio of upper-case letters of fake reviews is higher.
3. Non-fake reviews are more toxic since real users may be more “hate” or aggressive opinions of the game.
4. For similar reasons, fake reviews have more positive sentiemnts.

## Ethical Consideratioin
• Our first ethical consideration is that we only retrieved game reviews in English in order to visually justify our findings and label the reviews for classification and predictions. However, Dota2 is a popular game globally. Our data collection, in this case, may be less representative and can lead to biases in the sentiment analysis, predictive modeling, and spam classification sections.

• Secondly, the user name and the review is available without encryption, so if the user acciden- tally leaked his user game, his comment and attitudes toward other gamers may be revealed through our data.

## Limitation
• Our first limitation is we did not use all the data we scrapped due to constraints on compu- tational resources.

• The second limitation is we only gathered English reviews because English is best supported by other NLP packages.

