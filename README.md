# League of Legends Analysis: Is Azir a Better Mid Lane Champion?

by Steven Jiang

---

## Introduction

In this DSC80 project, I analyze a dataset of League of Legends esports matches to explore the performance of various champions, with a focus on Azir in the mid lane. The project includes cleaning and exploratory data analysis, assessment of missingness, and hypothesis testing.

---

## Cleaning and EDA

The dataset is a collection of data from League of Legends 2022 professional matches. Originally, the dataset has 149, 401 rows and 123 columns. However, not every column is relevant since we only want to work on the relative strength of Azir against other mid lane champions. Therefore, I selected some columns out of the 123 columns that can be potentially relevant. I also did some data cleaning so that the dataframe is easier for us to do further analysis. For example, I changed the `datacompleteness` data to Boolean values from strings.

Here are the columns I kept for the analysis and what they stand for:

- `gameid`: A unique identifier for each League of Legends match. It helps in distinguishing different games in the dataset.
- `datacompleteness`: Indicates whether the data recorded for a particular match is complete or incomplete. This helps in assessing the reliability of the data for analysis.
- `league`: Specifies the league in which the match was played. Different leagues often correspond to different regions or skill levels.
- `side`: Denotes which side (Blue or Red) the players or teams were on in a match. The side can impact game strategy and outcomes.
- `participantid`: A unique identifier for each participant (player or team) in a match. It helps in tracking individual or team performance across games.
- `position`: The in-game role or lane position of the player. Common positions include top, jungle, mid, bot, and support.
- `champion`: The name of the champion (character) chosen by a player for the match. Different champions have unique abilities and playstyles.
- `result`: The outcome of the match for the participant, typically represented as a win (1) or loss (0).
- `kills`: The number of enemy champions a player or team has killed during the match.
- `deaths`: The number of times a player or team has been killed by enemy champions.
- `assists`: The number of assists a player or team has, which are awarded for helping teammates kill enemy champions.
- `damagetochampions`: The total amount of damage dealt to enemy champions by a player or team.
- `damageshare`: The percentage of a team's total damage to enemy champions that was contributed by a particular player.
- `hextechs`: Could refer to the number of hextech items or objectives secured, such as Hextech Dragons in the game (this may vary depending on the dataset specifics).
- `earnedgold`: The total amount of in-game gold earned by a player or team during the match. Gold is used to purchase items that enhance abilities and stats.
- `golddiffat10`: The difference in gold earned between opposing teams or players at the 10-minute mark of the game. Indicates early game economic advantage.
- `xpdiffat10`: The difference in experience points (XP) between opposing teams or players at the 10-minute mark. Reflects early game leveling and progression advantage.

Also, we separated player's data and team's data. Here's the header of player's data called `data` after data cleaning:

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

This box plot compares damage share across different lanes, indicating the relative impact of players in different positions. We can see that mid is the second position that deals most damage right after bot.

<iframe src="assets/damage_share_lanes.html" width=800 height=600 frameBorder=0></iframe>

#### Plot 2: Average Damage Share Across Mid Lane Champions

Focusing on mid lane champions, this plot shows the average damage share for each champion, with a specific look at those with more than 1% pick rate. This is because we only want to compare popular mid champions and avoid unregular mid champions who were only used a few time and accidentally performed well. We can easily see that Azir is the third among all popular mid champions.

<iframe src="assets/avg_damage_share_mid_champions.html" width=800 height=600 frameBorder=0></iframe>

### Pivot table

Now we look at the relationship of several columns of the dataframe of popular mid lane champions at the same time, and we can find interesting relationships among side, champion, and win rate:

| side   |     Ahri |    Akali |     Azir |    Corki |    Galio |   LeBlanc |   Lissandra |   Orianna |     Ryze |   Seraphine |    Swain |    Sylas |   Syndra |   Taliyah |   Twisted Fate |   Veigar |      Vex |   Viktor |    Yasuo |    Yone |      Zoe |
|:-------|---------:|---------:|---------:|---------:|---------:|----------:|------------:|----------:|---------:|------------:|---------:|---------:|---------:|----------:|---------------:|---------:|---------:|---------:|---------:|--------:|---------:|
| Blue   | 0.551837 | 0.540486 | 0.527806 | 0.52451  | 0.483271 |  0.496528 |    0.518414 |  0.509128 | 0.474453 |    0.597561 | 0.58871  | 0.562716 | 0.512019 |  0.555556 |       0.552901 | 0.497872 | 0.507692 | 0.507692 | 0.506024 | 0.46789 | 0.553633 |
| Red    | 0.508872 | 0.478585 | 0.469534 | 0.500821 | 0.515021 |  0.453731 |    0.488608 |  0.459082 | 0.450475 |    0.496    | 0.494624 | 0.466599 | 0.443709 |  0.537129 |       0.560538 | 0.432056 | 0.477314 | 0.472537 | 0.426829 | 0.488   | 0.457912 |

We find that no matter which champion players use, playing on the blue side has a higher winning rate than on the red side. This phenomenon is interesting and it makes sense since the blue side pick champions first so that they can lock down the most OP champions earlier than the red side.

---

## Assessment of Missingness

### NMAR Analysis

In our dataset, we observe a pattern that suggests the missingness of certain columns, notably 'hextechs', is not occurring at random (NMAR). The dataset structure includes 12 columns for each match, detailing individual players and team-related statistics. We often see instances where player-specific data is absent while team data is present, or vice versa. This irregular pattern of missingness is influenced by the type of data recorded but does not show a direct one-to-one correspondence across columns, indicating that the missingness isn't systematically planned or designed.

Particularly for the 'hextechs' column, its absence in the data seems to correlate with specific leagues. It appears that not all leagues consistently track or report on hextech-related metrics. Consequently, the absence of 'hextechs' data might be linked to the league in which the match was played.

To address this and move towards Missing at Random (MAR) classification, additional data collection is essential. Specifically, gathering comprehensive hextech data from all matches across the leagues that previously did not report this information would be beneficial. This additional data would help fill the gaps caused by inconsistent tracking practices across different leagues, thereby standardizing the dataset and reducing the dependency of missingness on the league variable.

### Analysis of Hextechs Dependency on League

Now, for `team_data`, I investigate into the missingness of the `hextechs` data  and reveal its dependency on `league`. Here is the observed distribution when `hextechs` is missing:

|league      |    hextechs|
|:-----------|-----------:|
| LCKC       | 0          |
| LPL        | 0.4219     |
| NLC        | 0          |
| LVP SL     | 0          |
| PGC        | 0          |
| UL         | 0          |
| PRM        | 0          |
| LCK        | 0          |
| LFL        | 0          |
| LEC        | 0.0225443  |
| LCS        | 0.00107354 |
| LFL2       | 0          |
| GLL        | 0          |
| HM         | 0          |
| ESLOL      | 0          |
| EBL        | 0          |
| LPLOL      | 0          |
| PGN        | 0          |
| LCSA       | 0          |
| DDH        | 0          |
| TAL        | 0          |
| TCL        | 0          |
| CBLOL      | 0          |
| LCO        | 0          |
| LHE        | 0          |
| GL         | 0          |
| EL         | 0          |
| CBLOLA     | 0          |
| LMF        | 0          |
| VL         | 0          |
| SL (LATAM) | 0          |
| LLA        | 0          |
| HC         | 0          |
| LDL        | 0.505636   |
| LJL        | 0          |
| PCS        | 0          |
| VCS        | 0          |
| UPL        | 0          |
| LCL        | 0          |
| NEXO       | 0          |
| EUM        | 0          |
| LAS        | 0          |
| MSI        | 0          |
| LJLA       | 0          |
| CT         | 0          |
| WLDs       | 0.00751476 |
| CDF        | 0          |
| IC         | 0          |
| DCup       | 0.0413312  |

Here is the observed distribution when `hextechs` is not missing:

|league      |    hextechs|
|:-----------|-----------:|
| LCKC       | 0.0372155  |
| LPL        | 0          |
| NLC        | 0.0361764  |
| LVP SL     | 0.0231416  |
| PGC        | 0.053084   |
| UL         | 0.0262586  |
| PRM        | 0.0346652  |
| LCK        | 0.0441107  |
| LFL        | 0.0233305  |
| LEC        | 0.0189855  |
| LCS        | 0.0287145  |
| LFL2       | 0.0227638  |
| GLL        | 0.0191745  |
| HM         | 0.0144517  |
| ESLOL      | 0.0228582  |
| EBL        | 0.0174743  |
| LPLOL      | 0.0197412  |
| PGN        | 0.0140739  |
| LCSA       | 0.051006   |
| DDH        | 0.0197412  |
| TAL        | 0.0193634  |
| TCL        | 0.0208747  |
| CBLOL      | 0.0229527  |
| LCO        | 0.0200246  |
| LHE        | 0.0229527  |
| GL         | 0.0164353  |
| EL         | 0.0127515  |
| CBLOLA     | 0.0204024  |
| LMF        | 0.0301313  |
| VL         | 0.0160574  |
| SL (LATAM) | 0.0155852  |
| LLA        | 0.0176632  |
| HC         | 0.0153018  |
| LDL        | 0          |
| LJL        | 0.0202135  |
| PCS        | 0.0255974  |
| VCS        | 0.0305091  |
| UPL        | 0.0389157  |
| LCL        | 0.00151129 |
| NEXO       | 0.0182299  |
| EUM        | 0.0252196  |
| LAS        | 0.0214414  |
| MSI        | 0.00755644 |
| LJLA       | 0.00358931 |
| CT         | 0.00245584 |
| WLDs       | 0.0133182  |
| CDF        | 0.00689525 |
| IC         | 0.00708416 |
| DCup       | 0          |

I used TVD as the test statistic. The observed TVD is 0.9724261532426592. The permutation test yielded a significant p-value of 0.0. Here is the distribution of test statistic:

#### Empirical Distribution Plot for Hextechs Dependency on League

<iframe src="assets/hextechs_league_dependency.html" width=800 height=600 frameBorder=0></iframe>

Among players, missingness of `hextechs` does depend on `league`.

### Analysis of Hextechs Dependency on participantid

Also, for `team_data`, I investigate into the missingness of the `hextechs` data  and reveal its dependency on the `participantid`. Here is the observed distribution when `hextechs` is missing:
|participantid     |         hextechs|
|-----------------:|----------------:|
| 100              |             0.5 |
| 200              |             0.5 |

Here is the distribution of `participantid` when `hextechs` is not missing:

|participantid     |         hextechs|
|-----------------:|----------------:|
| 100              |             0.5 |
| 200              |             0.5 |

I used TVD as the test statistic. The observed TVD is 0.0. The permutation test yielded a insignificant p-value of 1.0. Here is the distribution of test statistic:

#### Empirical Distribution Plot for Hextechs Dependency on participantid

<iframe src="assets/hextechs_participantid_dependency.html" width=800 height=600 frameBorder=0></iframe>

Among players, missingness of `hextechs` does not depend on `participantid`.

---

## Hypothesis Testing

The primary question: Does Azir have a higher win rate than other popular mid champions? The analysis involved comparing Azir's win rate against other champions with more than 1% pick rate.

### Empirical Distribution of 10000 Sample Win Rates

Here is a table showing the average win rate and game count of each popular mid-lane champions. We can see that Azir only has an average win rate just above 50%, but we need a rigit hypothesis test to find out.

|              |   Average Win Rate |   Game Count |
|:-------------|-------------------:|-------------:|
| Ahri         |           0.531197 |         2933 |
| Akali        |           0.508244 |         1031 |
| Azir         |           0.501095 |         1826 |
| Corki        |           0.514386 |         1425 |
| Galio        |           0.498008 |          502 |
| LeBlanc      |           0.473515 |         1246 |
| Lissandra    |           0.502674 |          748 |
| Orianna      |           0.483903 |          994 |
| Ryze         |           0.463117 |         1559 |
| Seraphine    |           0.553633 |          289 |
| Swain        |           0.538899 |          527 |
| Sylas        |           0.511578 |         1857 |
| Syndra       |           0.47641  |          869 |
| Taliyah      |           0.547437 |          917 |
| Twisted Fate |           0.556202 |          516 |
| Veigar       |           0.461686 |          522 |
| Vex          |           0.491054 |         1006 |
| Viktor       |           0.489255 |         2187 |
| Yasuo        |           0.466667 |          330 |
| Yone         |           0.478632 |          468 |
| Zoe          |           0.505119 |          586 |

Null Hypothesis: Azir's winrate is the same with other mid lane champions with a pick rate above 1%
Alternative Hypothesis: Azir's winrate is higher than other mid lane champions with a pick rate above 1%
Significance Level: 5%
Test Stats: average win rate
The observed value is 0.5010952902519168

I simulated 10000 samples and this plot shows the distribution of sample win rates compared to Azir's observed win rate.

<iframe src="assets/sample_win_rates_distribution.html" width=800 height=600 frameBorder=0></iframe>

We get a p-value of 0.5623. Since it is larger than 0.05, so we fail to reject the null hypothesis at 5% significance level.

---

The findings suggest that Azir's win rate does not significantly differ from other mid lane champions at the 5% significance level, so we don't have enough evidence to say that Azir is generally a better mid champion than other popular mid picks.

---
