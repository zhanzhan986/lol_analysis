# League of Legends Analysis: Is Azir a Better Mid Lane Champion?

by Steven Jiang

---

## Introduction

In this DSC80 project, I analyze a dataset of League of Legends esports matches to explore the performance of various champions, with a focus on Azir in the mid lane. The project includes cleaning and exploratory data analysis, assessment of missingness, and hypothesis testing.

---

## Cleaning and EDA

The dataset initially contained numerous rows and columns. Relevant columns were selected for a focused analysis of Azir's performance. Data completeness was verified, and player-based data were separated from team-based data for more precise analysis. Here's the header after data cleaning:

| gameid                | datacompleteness   | league   | side   |   participantid | position   | champion   |   result |   kills |   deaths |   assists |   damagetochampions |   damageshare |   hextechs |   earnedgold |   golddiffat10 |   xpdiffat10 |
|:----------------------|:-------------------|:---------|:-------|----------------:|:-----------|:-----------|---------:|--------:|---------:|----------:|--------------------:|--------------:|-----------:|-------------:|---------------:|-------------:|
| ESPORTSTMNT01_2690210 | True               | LCKC     | Blue   |               1 | top        | Renekton   |        0 |       2 |        3 |         2 |               15768 |     0.278784  |        nan |         7164 |             52 |          -44 |
| ESPORTSTMNT01_2690210 | True               | LCKC     | Blue   |               2 | jng        | Xin Zhao   |        0 |       2 |        5 |         6 |               11765 |     0.208009  |        nan |         5368 |            485 |          432 |
| ESPORTSTMNT01_2690210 | True               | LCKC     | Blue   |               3 | mid        | LeBlanc    |        0 |       2 |        2 |         3 |               14258 |     0.252086  |        nan |         5945 |            162 |           71 |
| ESPORTSTMNT01_2690210 | True               | LCKC     | Blue   |               4 | bot        | Samira     |        0 |       2 |        4 |         2 |               11106 |     0.196358  |        nan |         6835 |            296 |          265 |
| ESPORTSTMNT01_2690210 | True               | LCKC     | Blue   |               5 | sup        | Leona      |        0 |       1 |        5 |         6 |                3663 |     0.0647631 |        nan |         2908 |            528 |         -587 |

### Univariate Analysis

#### Plot 1: Pick Rate of Champions in Mid Lane

This plot shows the frequency of champion picks in the mid lane, highlighting popular choices among players.

<iframe src="assets/mid_lane_pick_rate.html" width=800 height=600 frameBorder=0></iframe>

#### Plot 2: Distribution of Damage Share Across All Players

This histogram displays the distribution of damage share across all players in all matches, providing insights into player impact.

<iframe src="assets/damage_share_distribution.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis

#### Plot 1: Damage Share Across Different Lanes

This box plot compares damage share across different lanes, indicating the relative impact of players in different positions.

<iframe src="assets/damage_share_lanes.html" width=800 height=600 frameBorder=0></iframe>

#### Plot 2: Average Damage Share Across Mid Lane Champions

Focusing on mid lane champions, this plot shows the average damage share for each champion, with a specific look at those with more than 1% pick rate.

<iframe src="assets/avg_damage_share_mid_champions.html" width=800 height=600 frameBorder=0></iframe>

---

## Assessment of Missingness

### Analysis of Hextechs Dependency on League

An investigation into the missingness of the 'hextechs' data revealed its dependency on the league. The permutation test yielded a significant p-value.

#### Empirical Distribution Plot for Hextechs Dependency on League

<iframe src="assets/hextechs_league_dependency.html" width=800 height=600 frameBorder=0></iframe>

### Analysis of Hextechs Dependency on participantid

An investigation into the missingness of the 'hextechs' data revealed its dependency on participantid. The permutation test yielded a insignificant p-value.

#### Empirical Distribution Plot for Hextechs Dependency on participantid

<iframe src="assets/hextechs_participantid_dependency.html" width=800 height=600 frameBorder=0></iframe>

---

## Hypothesis Testing

The primary question: Does Azir have a higher win rate than other popular mid champions? The analysis involved comparing Azir's win rate against other champions with more than 1% pick rate.

### Empirical Distribution of 10000 Sample Win Rates

This plot shows the distribution of sample win rates compared to Azir's observed win rate.

<iframe src="assets/sample_win_rates_distribution.html" width=800 height=600 frameBorder=0></iframe>

---

The findings suggest that Azir's win rate does not significantly differ from other mid lane champions at the 5% significance level.

---
