# LoL-role-predictions
A project for DSC80 at UCSD predicting the role of League of Legends players based on their statistics.

Contributors: [Charisse Hao](https://www.linkedin.com/in/charisse-hao/) and [Nicole Zhang](https://www.linkedin.com/in/nicole-zhang-31a09122b/)

## Introduction
Welcome to Summoner’s Rift! [League of Legends (LoL)](https://en.wikipedia.org/wiki/League_of_Legends) is a popular online multiplayer battle arena game, with millions of active players worldwide. The game's massive player base makes it an excellent source of data for researchers and data scientists interested in exploring various aspects of the game, from player behavior to gameplay mechanics. 

Two teams, consisting of five players each, battle to destroy the opposing team's center base known as the Nexus. Each team's players fulfill a specific role on the team—selecting to play one of the five roles: top, jungle, middle, bottom, or support. As a continuation from our first project(https://charissehao.github.io/LoL-role-impact/), we decided to see if we could create a model that predicts which role someone picked based off of their game performance.

The dataset we used to conduct this analysis is the [2022 League of Legends Esports Stats dataset](https://drive.google.com/file/d/1EHmptHyzY8owv0BAcNKtkQpMwfkURwRy/view?usp=sharing) provided by Oracle's Elixir, a website that provides advanced statistics and analysis tools for the game. This dataset contains a comprehensive collection of data from professional League of Legends matches, including detailed information on player and team performance, game events, and match outcomes. The dataset contains information on thousands of matches, covering various tournaments and competitions.

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


## Table of Contents
- [Introduction](#introduction)
    - [Dataset Statistics and Definitions](#dataset-statistics-and-definitions)
- [Cleaning and EDA (Exploratory Data Analysis)](#cleaning-and-eda)
    - [Data Cleaning](#data-cleaning)
    - [Univariate Analysis](#univariate-analysis)
    - [Bivariate Analysis](#bivariate-analysis)
    - [Interesting Aggregates](#interesting-aggregates)
- [Framing the Problem](#framing-the-problem-problem-identification)
- [Baseline Model](#baseline-model)
- [Final Model](#final-model)
- [Fairness Analysis](#fairness-analysis)

## Cleaning and EDA (Exploratory Data Analysis) 

### Data Cleaning


## Framing the Problem: Problem Identification

## Baseline Model

## Final Model

## Fairness Analysis