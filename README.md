# competitive_lol_analysis_sklearn
DSC80 Project 5
Our previous analylsis of this dataset: https://aemoon03.github.io/Competitive-Lol-Analysis/

## Framing the Problem
Our prediction problem: how long will professional League of Legends games take? We will be using regression. Our response variable is “gamelength”, because this measures how long each game was. The metric we are using is R-squared because it is an appropriate evaluation metric for linear regression, as opposed to recall or precision which are better for classifiers. We know all of the information we need because the data we are analyzing is from 2022, which is already past. 

## Baseline Model
The features in our model are “teamname” and “gamelength”. “teamname” is nominal and “gamelength” is quantitative. Because “gamelength” is quantitative, we needed to perform one hot encoding on it. The R-squared of our model was about 0.04, which is a very poor performance. Such a low R-squared indicates that our linear regression model explains very little of our response variable.

## Final Model
We added the features csat15 and control wards bought, as we believe that they would be good indicators of how long a game would last, our logic being that if a player has low cs at the time, then he is likely to be far behind, meaning that he will likely lose fast, ending the game quickly. On the other end, a player with high cs mgiht have a larger amount of gold in order to buy items, which would help him close out the game faster. We believe that control wards bought was also a good feature to add in order to just judge the length of the game. Generally, the more control wards bought, the longer the game is. 

The hyperparameters we added were: fit_intercept, normalize, and n_jobs. We chose fit_intercept because it would be optimal to know if we use an intercept in our linear regression, normalize because we would need to know if we need to normalize the values that we are using, and n_jobs to figure out the number of jobs that is optimal for the linear regression to run. 

Our model's performance drastically improved in comparison to the Baseline Model. 

## Fairness Analysis
Our group X is tier one teams, or teams from the LCK, LEC, LPL, and LCS, and our group Y teams are all other teams. Our evaluation metric is R-squared.

Null Hypothesis: Our model is fair. Its precision for tier one teams and non-tier one teams are roughly the same, and any differences are due to random chance. 

Alternative Hypothesis: Our model is unfair. Its precision for non-tier one teams is lower than its precision for tier one teams. 

Our test-statistic was R-squared of our final model, and our significance level is 0.01. The resulting p-value was 0.0395. Because our p-value is less than the significance level, we would fail to reject the null hypothesis, meaning that our model's precision for tier one teams and non-tier one teams are roughly the same, and any differences are due to random chance. 
