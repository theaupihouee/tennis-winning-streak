# A Study of an Extraordinary Tennis Winning Streak 

## Project Description 

In 1999, Gasquet beats Nadal in Junior World Championship. 23 years later : 18-0 for Nadal against Gasquet. 

**How unlikely is the 18-0 streak of matches between Rafael Nadal and Richard Gasquet in the ATP circuit ? How much is there luck v. skill ?** 

To answer this question, the following steps have been carried out: 
1) In-depth analysis of winning streaks between all ATP players since 2000 
2) Implementation of SRS (Simple Rating System) and ELO models to conduct match simulations and quantify the unlikeliness of that neverending winning streak
3) Clustering analysis of Top 100 ATP players to compare the performances against R. Nadal of players identified as similar to Gasquet’s playing style 

## Main results 

### SRS and ELO Models

- The Simple Rating System (SRS) is a rating that evaluates the strength of a player compared to the average strength of players. The average SRS is set to 0 and players above 0 have a better rating than an average player and those with a negative rating perform worse than an average player 
- Each player has a server rating (S Rating) and a receiver rating (R Rating). All ratings are initialized randomly. 
- The models uses serve won points per match for each player and for every ATP matches  

![Updating SRS Ratings](images/srs_model.jpg)

- In the above formula, SWP_avg is the average service win percentage. Once the above probability has been computed, the probability of winning the match is calculated with probability trees to evaluate the odds of winning a game and a set 
- The major challenge is regarding data as there are few charted matches (detailed point-by-point data is collected manually). To solve that, linear regression has been used to extrapolate the number of points won using the match final scores. However, the results are not conclusive, as seen below 

- Regarding the ELO model, the  

![Elo Win Probability](images/elo_win_p.jpg)

![Updating Elo Ratings](images/elo_model.jpg)

![Models Accuracy](images/models_accuracy.jpg)

![Monte-Carlo Streaks Distribution](images/streak_distribution.jpg) 

![Cluster Comparison](images/cluster_comparison.jpg) 

## Data Sources 

- [ATP Matches Scores](https://github.com/JeffSackmann/tennis_atp) 
- [ATP Detailed Point-by-Point, Shot-by-Shot Matches](https://github.com/JeffSackmann/tennis_MatchChartingProject) 

## References 

- [The Match Charting Project: Quick Start Guide - Jeff Sackmann](http://www.tennisabstract.com/blog/2015/09/23/the-match-charting-project-quick-start-guide)
- [Weighted Elo rating for tennis match predictions](https://www.sciencedirect.com/science/article/abs/pii/S0377221721003234) 
- [Are differences in ranks good predictors for Grand Slam tennis matches?](https://www.sciencedirect.com/science/article/abs/pii/S0169207009002076) 
