
# The Summoner's Oracle: Predicting League of Legends Player Positions
An UCSD DSC80 project predicting the role of League of Legends players based on their in-game statistics.

Contributors: [Charisse Hao](https://www.linkedin.com/in/charisse-hao/) and [Nicole Zhang](https://www.linkedin.com/in/nicole-zhang-31a09122b/)


## Table of Contents
- [Introduction](#introduction)
    - [Dataset Statistics and Definitions](#dataset-statistics-and-definitions)
- [Data Cleaning](#data-cleaning)
- [Framing the Problem](#framing-the-problem-problem-identification)
- [Baseline Model](#baseline-model)
- [Final Model](#final-model)
- [Fairness Analysis](#fairness-analysis)


## Introduction
Welcome to Summoner’s Rift! [League of Legends (LoL)](https://en.wikipedia.org/wiki/League_of_Legends) is a popular online multiplayer battle arena game, with millions of active players worldwide. The game's massive player base makes it an excellent source of data for researchers and data scientists interested in exploring various aspects of the game, from player behavior to gameplay mechanics. 

Two teams, consisting of five players each, battle to destroy the opposing team's center base known as the Nexus. Each team's players fulfill a specific role on the team—selecting to play one of the five roles: top, jungle, middle, bottom, or support. As a continuation from a previous [project](https://charissehao.github.io/LoL-role-impact/), we decided to see if we could create a model that predicts which role someone played based off of their game performance.

The dataset we used to build our model is the [2022 League of Legends Esports Stats dataset](https://drive.google.com/file/d/1EHmptHyzY8owv0BAcNKtkQpMwfkURwRy/view?usp=sharing) provided by Oracle's Elixir, a website that provides advanced statistics and analysis tools for the game. This dataset contains a comprehensive collection of data from professional League of Legends matches, including detailed information on player and team performance, game events, and match outcomes. The dataset contains information on thousands of matches, covering various tournaments and competitions.

### Dataset Statistics and Definitions:
The dataset has a total of 149,232 rows and 123 columns. We cleaned the dataset to only include the data we needed for our analysis, so our dataframe consisted of 106,170 rows and 13 columns. Below are the definitions of the columns we used from this dataset.

| **Column Name**     | **Definition**                                               |
| ------------------- | ------------------------------------------------------------ |
| `gameid`            | game ID                                                      |
| `datacompleteness`  | indicates if the data for this match was complete or partial |
| `side`              | indicates which side the team was on ('blue' or 'red')       |
| `position`          | player’s position (more detail in table below)               |
| `kills`             | total kills per player                                       |
| `deaths`            | total deaths per player                                      |
| `assists`           | total assists per player                                     |
| `damagetochampions` | total damage dealt to other champions                        |
| `visionscore`       | vision granted and denied per player                         |
| `totalgold`         | total gold per player                                        |
| `earnedgoldshare`   | percent share of team’s total gold earned                    |
| `minionkills`       | total minions killed per player                              |
| `monsterkills`      | total monsters killed per player                             |

\* Note: we will be using the terms "role" and "position" interchangeably. 

| **Positions Abbreviation** | **Meaning** |
| -------------------------- | ----------- |
| *top*                      | top         |
| *jng*                      | jungle      |
| *mid*                      | middle      |
| *bot*                      | bottom      |
| *sup*                      | support     |


## Data Cleaning
As we are basing this prediction model off of similar data used in a previous [project](https://charissehao.github.io/LoL-role-impact/), we performed the same data cleaning steps.


## Framing the Problem: Problem Identification
**Prediction problem:** Can we predict a player’s role based on their in-game statistics?

This prediction problem requires building a multiclass classification model to classify players into one of five positions: middle, top, bottom, jungle, or support. In our case, `position` acted as the response variable as it is an essential variable in team composition and game strategy.

In a previous project, we explored the relationship between `position` and other variables such as `kills`, `assists`, `deaths`, `damagetochampions`, `totalgold`, etc. Since we found there is some indication of correlation between these variables and `position`, we were interested in exploring the possibility of using those variables to predict players’ positions.  

To evaluate our model, we used the precision metric. Precision helps to minimize the number of false positives, and by using this metric, it helped to ensure a higher accuracy when the model produced predictions. 

At the "time of prediction," we would only have access to the in-game statistics of a player, which would be used to predict their position. We will train the model using only these features, making sure to exclude any information that would not be available at the "time of prediction."



## Baseline Model
For our baseline model, we used a random forest classifier to predict the position based on three features: KDA, total damage to champions, and total gold. All of these features are quantitative variables, and KDA is derived from the combination of kills, deaths, and assists. No additional transformations or encodings were performed on these variables.

The performance of the model is reported as 0.4599, which shows that the model correctly predicts the position for 45.99% of the observations. This accuracy level is relatively low, and there is certainly room for improvement.

It is difficult to say definitively whether the current model is "good" or not without additional context. However, given that the model's accuracy is below 50%, it is safe to say that there is significant room for improvement. The model's performance can be improved by including additional relevant features or optimizing the parameters of the random forest classifier.


## Final Model
For our final model, several new features were added, including kills, deaths, assists, earned gold share, minion kills, monster kills, and vision score. These features provide additional insights into the data and can help the model better differentiate between different positions.

Kills, deaths, and assists were added on top of the KDA feature because they give more specific information about a player's performance. Only using KDA is essentially discarding the specific values of kills, deaths, and assists that make up the KDA calculation. This means that any information that was contained in the original KDA values (such as a player with a high number of assists but relatively few kills and deaths) is lost when the variable is transformed. Additionally, earned gold share, minion kills, monster kills, and vision score were included to capture information about the player's role within the team. For example, bottom and middle positions will have relatively higher gold share, support and jungle will have relatively lower minion kills, jungle and mid will have relatively higher monster kills, and support and jungle will have relatively higher vision score. For minion kills, monster kills, and vision score, we chose to binarize these statistics using the corresponding median for that column as the threshold. We chose the median as the threshold because the mean may be sensitive to outliers. As a result, minion kills, monster kills, and vision score are nominal data; KDA, kills, deaths, assists, and earned gold share are quantitative data.

The final model used a random forest classifier. One of the main reasons we chose the random forest algorithm is that it can handle a large number of input features and still maintain good performance. In the case of predicting a player's position, we have several input features to consider (such as kills, deaths, assists, gold, etc.), and the random forest algorithm is well-suited to handle this type of data. The random forest algorithm also has the ability to detect complex relationships between the input features and the output variable, which can help improve the accuracy of the model. Additionally, random forests are less prone to overfitting than some other algorithms, which is important when working with complex data. Our hyperparameters were tuned using grid search. The best hyperparameters were found to be a criterion of 'entropy', a max depth of 15, and a minimum sample split of 2. These hyperparameters were found using grid search, which allowed for an exhaustive search over different combinations of hyperparameters.

The final model achieved an accuracy of 0.7056, which is an improvement of approximately 20% over the baseline model. This suggests that the additional features and hyperparameter tuning were effective at improving the model's performance. Overall, the final model has a higher chance of correctly predicting a player's position based on the given data values.


## Fairness Analysis
Fairness analysis refers to the process of assessing whether a predictive model is biased or not against certain groups in a population. To evaluate the fairness of our final model, we assigned Group X to represent players on side ‘red’ and Group Y to represent players on side ‘blue’. We set up a null and alternative hypothesis to explore the possibility of bias:

**Null hypothesis:** Our model is fair. Its precision for teams on the blue side is roughly the same as the precision for teams on the red side, and any differences are due to random chance

**Alternative hypothesis:** Our model is unfair (biased). Its precision for teams on side blue is higher than its precision for teams on the red side. 

For our fairness analysis, we choose to use precision as our evaluation metric, with the test statistic being the difference in the precision of red and blue predictions. Our significance level was set at 0.05, and after running 500 permutation tests, we got a p-value of 0.136. 

<p style="text-align:center"><iframe src="assets/precision_diff.html" width=800 height=425 align='center' frameBorder=0></iframe></p>

In conclusion, based on the resulting p-value of 0.304 being greater than our significance level of 0.05, we fail to reject the null hypothesis. We do not have enough evidence to conclude that our model is unfair and its precision for teams on the blue side is higher than its precision for teams on the red side. Our conclusion seems to indicate our model is fair and that any observed differences in precision between the two groups are due to random chance.
