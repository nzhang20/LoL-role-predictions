
# LoL-role-predictions
A project for DSC80 at UCSD predicting the role of League of Legends players based on their statistics.

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

This prediction problem requires building a multiclass classification model to classify players into one of five positions: middle, top, bottom, jungle, or support. In our case, `position` acts as the response variable as it is an essential variable in team composition and game strategy.

In a previous project, we explored the relationship between `position` and other variables such as `kills`, `assists`, `deaths`, `damagetochampions`, `totalgold`, etc. Since we found there is some indication of correlation between these variables and `position`, we were interested in exploring the possibility of using those variables to predict players’ positions.  

To evaluate our model, we will use the precision metric. Precision helps to minimize the number of false positives, and by using this metric, it would help to ensure a higher accuracy when the model is producing predictions. 

At the "time of prediction," we would only have access to the in-game statistics of a player, which would be used to predict their position. We will train the model using only these features, making sure to exclude any information that would not be available at the "time of prediction."



## Baseline Model
For our baseline model, we used a random forest classifier to predict the position based on three features: KDA, total damage to champions, and total gold. All of these features are quantitative variables, and KDA is derived from the combination of kills, deaths, and assists. No additional transformations or encodings were performed on these variables.

The performance of the model is reported as 0.4588, which shows that the model correctly predicts the position for 45.88% of the observations. This accuracy level is relatively low, and there is certainly room for improvement.

It is difficult to say definitively whether the current model is "good" or not without additional context. However, given that the model's accuracy is below 50%, it is safe to say that there is significant room for improvement. The model's performance can be improved by including additional relevant features or optimizing the parameters of the random forest classifier.


## Final Model

## Fairness Analysis