# Multi-Source Data Analysis Project

Course project for CS 2064 at Virginia Tech. One notebook, three research questions, three kinds of data source: a REST API, web scraping and downloaded CSV files.

## Status by question

| Question | Source | Status |
|---|---|---|
| 1. How have average ratings and popularity of Pokémon video games changed over time? | RAWG Video Games API | Data pulled for 2000 to 2023 and averaged by year. |
| 2. How do data science job skills vary by industry and company size? | Indeed (web scraping) | Indeed returned HTTP 403, so the scraper collected nothing. The analysis runs on 8 hand-written sample listings. It demonstrates the method and is not a finding. |
| 3. How have NFL quarterback passing yards and completion percentages changed over the last decade? | Pro Football Reference CSVs, 2014 to 2023 | Complete. |

## Question 3: NFL passing trends

**Data.** Ten season-level passing tables from Pro Football Reference, one file per season.

**Method.**
1. Load each season file and add a `Year` column.
2. Concatenate into one DataFrame (35 columns).
3. Rename columns (`Cmp%` to `completion_pct`, `Yds` to `yards`, and so on) and convert key fields to numeric.
4. Group by year and average yards, completion percentage, touchdowns, interceptions, attempts and yards per game.
5. Plot yards per game and completion percentage on a dual-axis line chart.

**Findings.** Average yards per game per quarterback fell from about 122 in 2014 to about 106 in 2023, with a peak near 142 in 2015 and a rebound to about 114 in 2022. Completion percentage rose from 2014 to 2015, fell through 2017, rose through 2019, dipped slightly in 2020, fell in 2021, then rose in 2022 and 2023. These results are descriptive, not causal.

**Limitations.**
- Averages are per player and unweighted. Backups with few attempts count the same as starters, so the trend may reflect who appears in each season's file.
- Ten yearly data points and no statistical test.
- The two lines use different y-axis scales, so they should not be read as related.

## Known issues and next steps

- Question 1: ratings of 0 mean "unrated" and should be excluded. Add a chart and a written conclusion.
- Question 2: replace the blocked Indeed scrape with a source that permits access, or keep the sample data and the label above.
- Question 3: rerun with a minimum attempts filter (for example 100) or weight averages by attempts.
- The NFL cell reads its CSV files from `~/Downloads`, and the files are not in this repo, so the notebook does not run end to end for anyone else yet. Fixing this is the next step.

## Run it

```
export RAWG_API_KEY=your_key_here
pip install requests pandas numpy matplotlib seaborn beautifulsoup4 jupyter
jupyter notebook
```

The notebook reads the RAWG key from the `RAWG_API_KEY` environment variable and prompts for it if the variable is not set. A free key is available from rawg.io. Question 3 will not run until the CSV issue above is fixed.
