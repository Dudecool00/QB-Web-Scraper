# Findings: NFL Quarterback Play, 2014 vs. 2024

This write-up pulls together what the project found, a second look at those findings with a few extra checks, and the 2026 outlook. All numbers come from `2014_Season.csv` and `2024_Season.csv` (the top 50 passers by yards in each season, scraped from ESPN).

## The short version

Quarterbacks in 2024 completed passes more often but gained fewer yards doing it. Passing yards per game fell by about 24 yards among regular starters. Completion percentage rose by about 2.5 points. Each completion was worth less, which points to shorter, safer passing. The top of the league was also less separated from the middle than in 2014.

## Original findings

These are the conclusions drawn from the charts and the Stata summary:

1. **Passing yards per game are lower in 2024.** The box plots (`box_plots_qbr_ydsg.png`) show the whole 2024 distribution sitting below 2014.
2. **Average pass distance is lower in 2024.** In the CMP% vs. AVG scatterplot (`scatterplot_cmp_avg.png`), the 2024 line sits below the 2014 line: at the same completion percentage, 2024 quarterbacks gained fewer yards per attempt.
3. **Interceptions don't affect QBR as much in 2024.** In the correlation heatmaps (`heatmaps_cmp_ydsg_td_int_qbr.png`), the INT–QBR correlation drops from 0.29 in 2014 to 0.07 in 2024.
4. **QB performance was more variable in 2014.** The elite quarterbacks were more elite and the weakest were weaker, while 2024 was more bunched together.

## A second look

The 50-passer sample mixes full-season starters with backups who played a few games. In 2014, 16 of the 50 played fewer than 8 games. Backups add noise and can drive correlations on their own, so each finding was rechecked on **qualified passers** only, using the NFL's minimum of 14 attempts per team game (224 attempts in 2014, 238 in 2024). Differences were tested with Welch's t-test.

| Qualified passers | 2014 (n = 33) | 2024 (n = 36) | Change |
| --- | --- | --- | --- |
| Passing yards per game | 243.3 | 219.3 | −24.0 (p = 0.007) |
| Completion % | 62.9 | 65.3 | +2.4 (p = 0.015) |
| Yards per attempt (AVG) | 7.26 | 7.23 | −0.03 (p = 0.85) |
| Yards per completion | 11.56 | 11.09 | −0.47 |
| Interception rate (INT / ATT) | 2.50% | 2.26% | −0.24 |
| QBR, mean | 57.0 | 53.9 | −3.1 |
| QBR, standard deviation | 13.1 | 11.7 | −1.4 (Levene p = 0.50) |
| QBR, top 5 average | 76.0 | 71.1 | −4.9 |
| QBR, bottom 5 average | 37.1 | 35.3 | −1.8 |

How each original finding holds up:

1. **Lower yards per game: strongly supported.** This is the clearest result in the project. It holds in the full sample and among qualified passers, and it is statistically significant.
2. **Shorter passing: supported, with a better framing.** Yards per attempt barely moved. What changed is that completion percentage rose while yards per attempt stayed flat, so each completion gained less (11.6 → 11.1 yards). That is the signature of shorter, higher-percentage throws, which matches the scatterplot. Holding completion percentage fixed, 2024 passers gained 0.44 fewer yards per attempt across all 50 (p = 0.004), and 0.20 fewer among qualified passers (not significant).
3. **Interceptions and QBR: not supported once interceptions are measured as a rate.** Raw interception counts rise with attempts, and high-volume passers tend to be the better starters. That pushes the raw INT–QBR correlation upward and makes it mostly a measure of playing time. Using interception rate instead, the relationship with QBR is nearly identical in both seasons (r = −0.55 in 2014, −0.51 in 2024). A regression testing whether the interception-rate effect changed between seasons finds no meaningful difference (p = 0.41).
4. **More variable in 2014: directionally supported at the top.** Among qualified passers, the 2014 top five averaged about 5 QBR points higher than 2024's, while the bottom five were within 2 points. So "the elites were more elite" holds up. "The lows were much lower" is driven mostly by backups in the full sample, such as the 4.9 QBR outlier. The overall difference in spread is not statistically significant.

**New finding: completion percentage rose.** The project didn't call this out, but it is the second-strongest result: +3.1 points across all 50 passers (p = 0.003) and +2.4 among qualified passers. Together with the yards-per-completion drop, it supports one story: offenses traded downfield yardage for efficiency.

## Data notes

- **The 2014 passer rating (RTG) column is incorrect.** It contains only five distinct values (26 of 50 rows read 56.3), which suggests a scraping or column-alignment issue. Recomputing passer rating from the 2014 completions, yards, touchdowns and interceptions gives a mean of 86.6, compared with 90.1 in 2024. RTG is not used in any chart, so no conclusions are affected, but the column should be re-scraped or dropped.
- **The Stata log covers the 2024 season only.** Running the same `ci means` on the 2014 data would give matching confidence intervals for both seasons.
- **Sample definition.** "Top 50 by passing yards" pulls in different numbers of backups each year. Filtering to qualified passers, as above, makes the two seasons more comparable.

## 2026 outlook

The original prediction holds up well against these checks. Two seasons is a short window compared with the ten-year gap studied here, so a sharp change is unlikely. The forecast:

- Yards per game decline slightly, by roughly 1–2%, if offensive and defensive schemes don't change.
- Mean QBR stays steady.
- The spread of QBR widens by 1–2%.

The trends found here suggest what to watch: whether completion percentage keeps climbing and yards per completion keeps falling. If both continue, the yards-per-game decline should continue with them. One caution on the spread prediction: the qualified-passer data shows the spread narrowing from 2014 to 2024, so a widening would mean that trend reversing.
