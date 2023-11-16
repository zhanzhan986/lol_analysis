# League of Legends Analysis: Is Azir a Better Mid Lane Champion?

by Steven Jiang

---

## Introduction

In this DSC80 project, I analyze a dataset of League of Legends esports matches to explore the performance of various champions, with a focus on Azir in the mid lane. The project includes cleaning and exploratory data analysis, assessment of missingness, and hypothesis testing.

---

## Cleaning and EDA

The dataset initially contained numerous rows and columns. Relevant columns were selected for a focused analysis of Azir's performance. Data completeness was verified, and player-based data were separated from team-based data for more precise analysis.

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

---

## Hypothesis Testing

The primary question: Does Azir have a higher win rate than other popular mid champions? The analysis involved comparing Azir's win rate against other champions with more than 1% pick rate.

### Empirical Distribution of 10000 Sample Win Rates

This plot shows the distribution of sample win rates compared to Azir's observed win rate.

<iframe src="assets/sample_win_rates_distribution.html" width=800 height=600 frameBorder=0></iframe>

---

The findings suggest that Azir's win rate does not significantly differ from other mid lane champions at the 5% significance level.

---
