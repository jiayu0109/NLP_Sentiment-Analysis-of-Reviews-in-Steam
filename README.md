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
## RQ2: What is the relationship between toxicity level of reviews and user gaming time?
## RQ3: What are typical linguistic patterns of fake reviews in the Steam Community?



## Limitations
We only collected English reviews that are easier to process with existing NLP packages. But Dota2 has players across the world. The reviews we collect may  not be  representative for the entire player base. 
