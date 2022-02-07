# THE LEAGUE OF LEGENDS RANKED MATCHES ANALYSIS PROJECT
**Conducted by Yulin Hong and Angela Chen**
## Introduction

The League of Legends (LOL) is a multiplayer online battle arena game developed by Riot in 2009. In each match, 10 players are divided into two teams, red and blue. In its most played mode, the Summoner’s Rift, each player needs to control a character known as champion to defend their team’s base and invade the other half of the map. A team wins by destroying the Nexus in front of the enemy team’s base.

League of Legends has been the most played game in the world since 2012. Each year it will hold a ranked season where players play with or against others that share a similar level of gaming abilities. The annually ranked seasons first started in July 2010 and right now LOL is approaching the end of season 11. During a ranked season, the points will be added or deducted if a player succeeds or loses in one rank game. The final points will decide the annual ranking of a player. Currently, the League of Legends ranking system has 9 tires and 4 divisions within each tire. However, before season 9 there were only 7 tires and 5 divisions in each tire.

In this project, we used [the League of Legend Ranked Matches dataset](https://www.kaggle.com/paololol/league-of-legends-ranked-matches?select=matches.csv) to explore the hidden information behind ranked games. Using classification models, we predicted the outcome of a game using game statistics such as the kill death assist ratio. We also conducted cluster analysis on the matches. By mapping the clustering result to the tires based on clusters’ characteristics and size, we then analyzed the similarity and differences among tires.

Since the origin dataset comprised 184,070 ranked solo games across various seasons and platforms, we restrict our scope of work to analyzing North American platform Season 8 matches. The python code that used to process the origianl kaggle data can be find in the [preprocessing](https://github.com/yu1inhong/lol_ranked_matches_analysis/tree/main/preprocessing) folder. However, the idea behind this project can be applied to the whole dataset.
