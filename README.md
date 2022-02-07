# THE LEAGUE OF LEGENDS RANKED MATCHES ANALYSIS PROJECT

<p align="center">
  <img src="https://lh3.googleusercontent.com/WebglHOYlW-2P7ADP9oUSSrgy12PHyAE6GP_jmJkQOZZ1XH7Pa_7216EK2qS7iJFvncqOaDjg40BrYdzPbB9qNwn" alt="drawing" width="600"/>
<p align="center">
    Conducted by Yulin Hong and Angela Chen
</p>

## Introduction

The League of Legends (LOL) is a multiplayer online battle arena game developed by Riot in 2009. In each match, 10 players are divided into two teams, red and blue. In its most played mode, the Summoner’s Rift, each player needs to control a character known as champion to defend their team’s base and invade the other half of the map. A team wins by destroying the Nexus in front of the enemy team’s base.

League of Legends has been the most played game in the world since 2012. Each year it will hold a ranked season where players play with or against others that share a similar level of gaming abilities. The annually ranked seasons first started in July 2010 and right now LOL is approaching the end of season 11. During a ranked season, the points will be added or deducted if a player succeeds or loses in one rank game. The final points will decide the annual ranking of a player. Currently, the League of Legends ranking system has 9 tires and 4 divisions within each tire. However, before season 9 there were only 7 tires and 5 divisions in each tire.

In this project, we used [the League of Legend Ranked Matches dataset](https://www.kaggle.com/paololol/league-of-legends-ranked-matches?select=matches.csv) to explore the hidden information behind ranked games. Using classification models, we predicted the outcome of a game using game statistics such as the kill death assist ratio. We also conducted cluster analysis on the matches. By mapping the clustering result to the tires based on clusters’ characteristics and size, we then analyzed the similarity and differences among tires.

Since the origin dataset comprised 184,070 ranked solo games across various seasons and platforms, we restrict our scope of work to analyzing North American platform Season 8 matches. The python code that used to process the origianl kaggle data can be find in the [preprocessing](https://github.com/yu1inhong/lol_ranked_matches_analysis/tree/main/preprocessing) folder. However, the idea behind this project can be applied to the whole dataset.

**The following analysis section are based on the R code in [lol_ranked_matches_analysis](https://github.com/yu1inhong/lol_ranked_matches_analysis/blob/main/lol_ranked_matches_analysis.R). And the dataset used in the code can be find in [dataset](https://github.com/yu1inhong/lol_ranked_matches_analysis/tree/main/dataset) folder.**

## Data Preprocessing
The original dataset comprised of 7 tables, but the datasets were manipulated into two final matches statistics tables. After extracting the match games data for games in the North American area and Season 8, we then combine the tables of matches, participants, general statistics, and team statistics by matching each player in the participants and general statistics tables using their match ID in matches and team statistics tables. Note that our project does not analyze the performance of individual players, but the performance of the whole team (comprised of 5 players) in a match. Hence, after extracting all the data, we then group the statistics by match ID and team ID (an indicator of the blue or red team) and calculate the average value of each continuous statistics variable within a team of each match. Binary variables were not included in the process of averaging because the binary variable (such as first blood) are already variables that indicate the team status.

The dataset obtained from the previous step still contains over 50 predictors, but most of them are irrelevant such as items or some of them are interdependent, such as total damage dealt and magical damage dealt. Therefore, we removed all the irrelevant predictors as well as the predictors that depend on others. The final dataset consists of 23 predictors.

## Descriptive Analysis
Boxplots and histograms were used to visualize the distribution of these predictors. The predictor KDA represents the kill death assist ratio, and most of the teams have a KDA ratio of around 2. This means the number of kills or assists is twice as many as death. Then, total damage dealt, total damage to champion and total damage taken are bell-shaped continuous predictors with a little outlier. The gold earned and gold spent both have a mean of around $12000, meaning players usually spend all the gold they earn. Next, the champion level is right-skewed, meaning most of the teams have a high champion level. In contrast, inhibitor kill, baron kill, dragon kill, are left-skewed, meaning most of the teams killed fewer inhibitors, barons, and dragons. Lastly, the duration is also bell-shaped, and the average matches lasted for 2000 seconds (about 33 and a half minutes).

<p align="center">
  <img src="https://github.com/yu1inhong/lol_ranked_matches_analysis/blob/main/image/Screen%20Shot%202022-02-07%20at%209.39.39%20AM.png" alt="drawing" width="600"/>
</p>
<p align="center">
    Sample Boxplot and Histogram
</p>

A correlation matrix was created to examine the multicollinearity issue. Duration, champion level, gold spent, gold earned, the total damage to champions, and total damage dealt tend to have a relatively high correlation among each other. On the other hand, harry kill is uncorrelated to any other predictors or with the target variable. Therefore, in the classification model, gold earned, gold spent, duration, and harry kills are not considered.

<p align="center">
  <img src="https://github.com/yu1inhong/lol_ranked_matches_analysis/blob/main/image/Screen%20Shot%202022-02-07%20at%209.52.56%20AM.png" alt="drawing" width="600"/>
</p>
<p align="center">
    Correlation Matrix
</p>
