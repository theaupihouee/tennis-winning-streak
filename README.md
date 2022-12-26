# A Study of an Extraordinary Tennis Winning Streak 

## Project Description 

In 1999, Gasquet beats Nadal in Junior World Championship. 23 years later : 18-0 for Nadal against Gasquet. 

**How unlikely is the 18-0 streak of matches between Rafael Nadal and Richard Gasquet in the ATP circuit ? How much is there luck v. skill ?** 

To answer this question, the following steps have been carried out: 
1) In-depth analysis of winning streaks between all ATP players since 2000 
2) Implementation of SRS (Simple Rating System) and ELO models to conduct match simulations and quantify the unlikeliness of that neverending winning streak
3) Clustering analysis of Top 100 ATP players to compare the performances against R. Nadal of players identified as similar to Gasquet’s playing style 

*Note : All streaks described below are streaks between two players. We are not talking about winning matches in a row against different opponents* 

## Main results 

- Below is a comparison of the accuracy of the three models that we studied (SRS, ELO and a benchmark) 
- For the benchmark: The player with the best ATP ranking is predicted to win. However, no win probabilities inferred 
- The predictions have been made between 2004 and 2022. **Each year, the ratings are computed using the data for the given year and predictions are made for the next year using these ratings and compared to the actual outcomes of ATP matches** 

![Models Accuracy](images/models_accuracy.jpg)

- We notice a poor accuracy for the SRS model (close to a random predictor). This is mainly because of a lack of data : there are very few charted matches containing point-by-point data (manual process). Even trying to extrapolate the number of points won with linear regression using the match final score was not conclusive. In the end, there was not enough consistent data to efficiently train the model 
- The ELO model has a good accuracy, quite similar to the benchmark, although slightly better. The real advantage of the ELO model compared to the benchmark is that we can infer win probabilities for each match, which will be crucial when conducting Monte Carlo simulations 

- Below is the distribution of winning streaks obtained by running 90,000 Monte Carlo simulations using the ELO model 
- Simulations of confrontations between 10 players (total of 90 combinations), and for each combination, we run 1,000 simulations. The 10 players contain Nadal and Gasquet, as well as other players that had the same career length as the duo. 
- We have replicated the same configuration as the real events : frequence_matches = {2004:1, 2005:2, 2006:0, 2007:1, 2008:2, 2009:1, 2010:0, 2011:3, 2012:0, 2013:2, 2014:1, 2015:1, 2016:0, 2017:1, 2018:1, 2019:0, 2020:0, 2021:1, 2022:1} That means that in 2004, Nadal and Gasquet played their first match, in 2005 they played two matches, etc. For each of these matches, we used the ELO ratings of the players at that time 
- **For each simulation, the outcome is a list of 0 or 1 with a length of 18** (for the 18 matches played in their career, and 1 means that Nadal won the match). Each position in the list has a specific probability of being 1 or 0. We were thus particularly interested in the case where the list was filled with ones => streak of 18 wins. **Given that list, we recorded the longest streak of wins**

![Monte-Carlo Streaks Distribution](images/streak_distribution.jpg) 

- To obtain the graph above, we made the **null hypothesis of no streakiness : all ordering of confrontations between two players are equally likely. The outcome of a match has no impact over the outcome of the next one** 
- We obtain a **percentage of 1.16% where the maximum streak is 18**. This corresponds to a **p-value (probability of observing such event under the null hypothesis)** 
- We thus **reject the null hypothesis (p-value < 0.05) which means that there is some streakiness**. 
- **Overall, there is of course some luck involved in this extraordinary event, but it required a lot of skill from Nadal to actually make it possible** 

- Let's go further in the analysis by looking at **how skills may have impacted this event** 
- We performed some clustering to find players having a similar style to Gasquet. We used the work made by Johnattan Ontiveros to fetch Gasquet's cluster, which is **"All-Court" (players that are good with all types of shots and in all positions) and completed it by filtering players that were righ-handed with a one-handed backhand**. 
- We then compared Nadal's performances overall and against the clustered: 

![Cluster Comparison](images/cluster_comparison.jpg) 

- We notice better performances against players of the cluster than overall (both for win percentage and max streak average) 
- A further possible explanation to that 18-0 streak is thus that **the "skill" part can be explained by a difference in style between Gasquet and Nadal that favors the latter**

## Data Sources 

- [ATP Matches Scores](https://github.com/JeffSackmann/tennis_atp) 
- [ATP Detailed Point-by-Point, Shot-by-Shot Matches](https://github.com/JeffSackmann/tennis_MatchChartingProject) 

## References 

- [The Match Charting Project: Quick Start Guide - Jeff Sackmann](http://www.tennisabstract.com/blog/2015/09/23/the-match-charting-project-quick-start-guide)
- [Weighted Elo rating for tennis match predictions](https://www.sciencedirect.com/science/article/abs/pii/S0377221721003234) 
- [Are differences in ranks good predictors for Grand Slam tennis matches?](https://www.sciencedirect.com/science/article/abs/pii/S0169207009002076) 
- [Sorting strokes : Classifying tennis players based on stats and style](https://harvardsportsanalysis.org/2021/07/sorting-strokes-classifying-tennis-players-based-on-stats-and-style/)
