<div align="center">

# ⚽ FIFA World Cup Data Analysis (1930 – 2022)
### A Comprehensive Statistical & Visual Deep-Dive into 92 Years of Football History

`Analysis Type: Exploratory Data Analysis` · `Domain: Sports Analytics` · `Scope: 1930–2022` · `Editions Covered: 22`

`Datasets: 3` · `Total Matches Analyzed: 964` · `Teams Tracked: 211` · `Status: ✅ Complete`

---

</div>

> 📌 **About this report**: This document is a professional restructuring and narrative expansion of a Jupyter Notebook that analyzed three interconnected FIFA World Cup datasets — historical champions (1930–2022), the October 2022 FIFA World Ranking, and match-level results spanning nine decades. It is designed to be both a technical EDA reference and a readable sports-analytics story.

---

## 🧾 Executive Summary

- 🏆 **Brazil is the undisputed king of the tournament** — the only nation with 5 titles, 7 final appearances, and the record for both most home goals scored and most matches played (103).
- 🥇 **Just Fontaine's 13-goal haul at the 1958 World Cup** remains the most goals scored by a single player in one edition — a record that has stood for over 65 years and is unlikely to ever be broken under the current match-count format.
- 📈 **Tournament scale has grown four-fold**: from 18 matches in 1930 to a steady 64 matches per edition since 1998, reflecting the expansion from 13–16 teams to 32.
- 🇺🇸 **The 1994 USA World Cup is the attendance outlier** — despite having fewer matches (52) than every edition from 2002 onward (64), it recorded the **highest average attendance per match (68,991)** in tournament history, a testament to American stadium capacity and market scale.
- 🌍 **FIFA rankings (Oct 2022) show real mobility**: 36.5% of the 211 ranked teams improved their position, 32.2% dropped, and only 31.3% held steady — indicating the ranking table is anything but static.

---

## 📚 Table of Contents

1. [Introduction](#1-introduction)
2. [Data Overview & Exploratory Data Analysis](#2-data-overview--exploratory-data-analysis-eda)
3. [Key Findings & Insights](#3-key-findings--insights)
4. [Visualizations Analysis](#4-visualizations-analysis)
5. [Advanced Analysis & Statistical Insights](#5-advanced-analysis--statistical-insights)
6. [Conclusions & Recommendations](#6-conclusions--recommendations)
7. [Limitations & Future Work](#7-limitations--future-work)
8. [Appendix](#8-appendix)

---

## 1. Introduction

### 🎯 Objective of the Analysis

The purpose of this analysis is to build a data-driven understanding of FIFA World Cup history by answering questions such as:

- Which nations and players have historically dominated the tournament?
- How has the World Cup evolved in scale (teams, matches, attendance) since 1930?
- What patterns exist in scoring, home/away performance, and defensive resilience?
- How does the current FIFA global ranking landscape (as of October 2022) compare to historical World Cup success?

The analysis blends **historical tournament records** with a **snapshot of current national team rankings** and **granular match-level statistics**, creating a 360° view of international football performance.

### 🗂️ Dataset Description

Three distinct datasets were combined to power this analysis:

| Dataset | File | Rows | Key Columns | Time Span |
|---|---|---|---|---|
| 🏆 World Cup Champions | `world_cup.csv` | 22 | Year, Host, Teams, Champion, Runner-Up, Top Scorer, Attendance, AttendanceAvg, Matches | 1930 – 2022 |
| 🌍 FIFA World Ranking | `fifa_ranking_2022-10-06.csv` | 211 | Team, Association, Rank, Previous Rank, Points, Previous Points | Snapshot: Oct 6, 2022 |
| ⚽ Match Results | `matches_1930_2022.csv` | 964 | Home/Away Team, Score, Managers, Captains, Attendance, Venue, Round, Referee, Goals, Cards, Substitutions | 1930 – 2022 |

> 💡 **Note:** Each of the 22 World Cup editions is represented once in the champions dataset (one row per tournament), while the matches dataset captures **every individual match** ever played across all 22 editions — 964 matches in total.

---

## 2. Data Overview & Exploratory Data Analysis (EDA)

### 🔍 Shape, Duplicates & Missing Values

<details>
<summary><strong>📊 Click to expand: Dataset-by-dataset EDA summary</strong></summary>

**Champions Dataset (`world_cup.csv`)**
- 22 rows × 8 original columns
- Top scorer field required parsing (e.g., `"Kylian Mbappé - 8"`) — split into player name and goal count via string operations
- No explicit missing-value or duplicate-check was needed given the dataset's small, curated size

**FIFA Ranking Dataset (`fifa_ranking_2022-10-06.csv`)**
- 211 rows × 7 original columns (→ 6 after dropping the redundant `team_code` column)
- ✅ **Zero duplicate rows**
- ✅ **Zero missing values** across all columns — a fully clean dataset
- `team` and `rank` both contain exactly 211 unique values, confirming a one-to-one team-to-rank mapping

**Matches Dataset (`matches_1930_2022.csv`)**
- 964 rows × 44 original columns
- ✅ **Zero duplicate rows**
- ⚠️ **Significant missingness** in advanced/modern metrics: columns like `home_xg`, `away_xg`, `home_penalty`, `away_penalty`, and shootout/red-card detail fields were missing in **more than 50% of rows** — a direct consequence of expected-goals (xG) and detailed event tracking only being recorded in recent tournaments
- Columns exceeding the 50% missing-value threshold were **programmatically dropped**, reducing the working dataset to a leaner, higher-quality set of 25 columns

</details>

#### 📉 Missing Data Visualization

> The notebook produced a horizontal bar chart plotting the **percentage of missing values per column** in the matches dataset. Columns such as `home_xg`, `away_xg`, `home_penalty`, and `away_penalty` towered above the 80–95% missing mark, while core fields (`home_team`, `away_team`, `home_score`, `away_score`, `Date`, `Year`) showed **0% missingness** — confirming the foundational scoreline data is fully reliable even where advanced analytics fields are not.

**Key Takeaway Box:**
> ✅ **Data Quality Verdict**: All three datasets are duplicate-free. The ranking dataset is pristine (no nulls). The matches dataset requires selective column-pruning due to historical data-collection gaps — a completely expected pattern for a 92-year time series where modern analytics (xG, VAR-era penalty tracking) simply didn't exist for early tournaments.

### 📈 Statistical Summary (FIFA Ranking Points)

| Metric | Value | Team |
|---|---:|---|
| Maximum Points | **1,841.30** | 🇧🇷 Brazil |
| Minimum Points | **762.22** | 🇸🇲 San Marino |
| Average Points (211 teams) | **1,220.69** | — |

This ~1,079-point spread between #1 and #211 illustrates the steep competitive gradient in international football — Brazil's points total is roughly **2.4× higher** than San Marino's.

---

## 3. Key Findings & Insights

### 🏆 Historical Performance of Top Teams

- **Brazil** leads all-time World Cup wins with a commanding margin, followed by **Italy**, then **Argentina** (whose 2022 Qatar triumph pushed them to third), with **Germany/West Germany**, **France**, and **Uruguay** rounding out the multi-time-champion tier.
- When **runner-up finishes** are added to titles, **Brazil (7 total final appearances)** still tops the list, but **Argentina and Italy (6 each)** and **West Germany (5)** show remarkable consistency in reaching football's biggest stage — even when they didn't lift the trophy.
- **Argentina, West Germany, and the Netherlands** share the unfortunate distinction of the most runner-up finishes (3 each) — the Netherlands notably has *never* won a World Cup despite three final appearances, making it the most successful "bridesmaid" nation in tournament history.

### ⚽ Goal Trends & Scoring Patterns

- The **Golden Boot leaderboard** is dominated by an interesting mix of eras: **Just Fontaine (13 goals, 1958)** and **Sándor Kocsis (11 goals, 1954)** from football's early "high-scoring" decades sit well above modern top scorers like **Ronaldo and Mbappé (8 goals each)** — reflecting how tactical sophistication and defensive organization have tightened scoring ceilings over time.
- **Gerd Müller (10 goals, 1970)** and **Eusébio (9 goals, 1966)** further reinforce that the 1950s–1970s were the golden age of prolific individual scoring at the World Cup.
- **Brazil is the top home-scoring nation** by a wide margin (~190 goals), nearly 60% more than second-placed Argentina — underscoring Brazil's attacking identity across generations of teams.
- In **away scoring**, the gap narrows considerably: **Brazil, France, and Spain** are closely bunched near the top (~47–48 goals each), suggesting elite attacking talent travels well regardless of tournament venue.

### 🏟️ Tournament Scale & Attendance Analysis

- Match count per edition has grown in three distinct "eras":
  - **1930–1978**: 17–38 matches (13–16 team formats)
  - **1982–1994**: 52 matches (24-team format)
  - **1998–2022**: 64 matches (32-team format, now stable)
- Despite fewer matches, **1994 (USA)** recorded the tournament's **highest-ever average attendance per match (68,991)** — even surpassing every edition from 2002 to 2022, each of which hosted 12 more matches. This is best explained by the sheer scale of American stadiums and the tournament's novelty in a market with enormous population and stadium capacity.
- **Host nation analysis** shows only five countries have hosted twice: **Brazil, Mexico, Germany, Italy, and France** — every other host nation (17 countries) has hosted exactly once, reflecting FIFA's rotation policy and the immense infrastructure cost of hosting.

### 🏠 Home Advantage & Match-Level Analysis

- **Brazil has played more World Cup matches (103) than any other nation**, roughly 15 more than second-placed Argentina (88) — a direct function of their unmatched qualification consistency (they've never failed to qualify) combined with deep tournament runs.
- At the opposite end, nations like **Dutch East Indies (1 match)**, **Zaire, Trinidad and Tobago, UAE, Qatar, and Iceland (3 matches each)** represent single-appearance or early-elimination stories — snapshots of football's global underdogs.
- **Defensive resilience** tells a different story than attacking output: Brazil, Argentina, and Mexico also appear among the **most goals conceded**, a natural consequence of playing the most matches and often facing the toughest knockout-stage opposition.
- Teams like **Angola, Israel, and Iraq** show the **fewest goals conceded**, largely because of their limited number of tournament appearances rather than superior defense — a reminder that raw counts must always be read alongside match volume.

### 🌍 Player & Nation Deep-Dives

- **Just Fontaine's case study** (highlighted explicitly in the source notebook) is particularly compelling: despite his record 13 goals, **France finished as runner-up in 1958**, losing the final to Brazil — proving individual brilliance doesn't guarantee team success.
- **1994's anomaly** (fewer matches, more attendance) was specifically investigated in the notebook and attributed to the United States' large population, stadium infrastructure, and multi-ethnic fan base drawing record crowds despite the smaller 24-team format.

> **🔑 Key Takeaway**: Team success at the World Cup is multidimensional — trophy counts, final appearances, goals scored, goals conceded, and matches played each tell a different part of the story. Brazil consistently leads on nearly every dimension, but the runner-up and scoring-trend data reveal deep nuance beneath the top-line titles table.

---

## 4. Visualizations Analysis

Below is a structured breakdown of every major visualization produced in the source notebook, along with the insight each one delivers.

### 📊 4.1 Top Scorers and Their Goals (Horizontal Bar Chart)

![Top Scorers and Their Goals](images/top_scorers_goals.png)

- **What it shows**: Every World Cup's top scorer plotted against their goal tally, ordered chronologically (2022 → 1930).
- **Key takeaway**: Just Fontaine's 13-goal 1958 campaign is a clear outlier at the top of the range; most modern top scorers cluster around 6–8 goals.
- **Insight**: The chart visually confirms a *declining ceiling* for individual scoring, driven by tighter defensive tactics and fewer total matches per player compared to the mid-20th century.
- **Suggested improved title**: *"Golden Boot Winners Across 22 World Cups: The Fontaine Anomaly"*

### 🏆 4.2 Teams with the Most World Cup Wins

![World Cup Wins by Team](images/wins_by_team.png)

- **What it shows**: A ranked bar chart of every World Cup–winning nation and their total title count.
- **Key takeaway**: Brazil sits clearly above the pack, followed by Italy and Argentina, with a tightly bunched second tier (Germany, France, Uruguay, West Germany).
- **Insight**: Only 8 nations have *ever* won the World Cup in 22 editions — a striking concentration of success at the very top of international football.
- **Suggested improved title**: *"The Exclusive Club: 8 Nations, 22 Titles"*

### 🥈 4.3 Teams with the Most Runner-Up Finishes

![Runner-Up Finishes](images/runner_up_finishes.png)

- **What it shows**: Nations ranked by number of World Cup final losses.
- **Key takeaway**: Argentina, West Germany, and the Netherlands share the top spot with 3 runner-up finishes each.
- **Insight**: The Netherlands' presence at the top — with **zero titles** — makes them the most notable "nearly team" in World Cup history.
- **Suggested improved title**: *"So Close: The Nations That Reached the Final Most, Without the Trophy"*

### 🎯 4.4 Teams with the Most World Cup Final Appearances

![Final Appearances](images/final_appearances.png)

- **What it shows**: Combined champion + runner-up appearances per nation, merging the two prior charts into one aggregate view.
- **Key takeaway**: Brazil (7), Argentina and Italy (6 each), and West Germany (5) form the tournament's true "final four" of consistency.
- **Insight**: This combined metric is arguably a better proxy for *sustained excellence* than raw title counts alone, since it rewards teams that consistently reach football's biggest match.
- **Suggested improved title**: *"The Finalist Elite: Who Reaches the Big Match Most Often?"*

### 🎟️ 4.5 Total Attendance of FIFA World Cup Versions

![Total Attendance](images/total_attendance.png)

- **What it shows**: Aggregate tournament attendance by year, 1930–2022.
- **Key takeaway**: A clear upward trend from under 600,000 total attendees in 1930 to well above 3 million from the 1990s onward.
- **Insight**: Growth in total attendance tracks closely with the expansion of tournament size (more teams → more matches → more cumulative attendance).
- **Suggested improved title**: *"From Uruguay to Qatar: The Growth of World Cup Attendance"*

### 📐 4.6 Attendance Average of FIFA World Cup Versions

![Average Attendance](images/average_attendance.png)

- **What it shows**: Per-match average attendance by year — a normalized view that controls for the varying number of matches.
- **Key takeaway**: **1994 (USA) stands out dramatically**, with an average of ~68,991 attendees per match, the highest in tournament history, even above recent editions in Qatar, Russia, and Brazil.
- **Insight**: This is the notebook's most important discovery — raw match counts (4.7 below) don't tell the full attendance story.
- **Suggested improved title**: *"The 1994 Anomaly: Why the USA World Cup Still Holds the Attendance Record"*

### 🗓️ 4.7 Number of Matches in FIFA World Cup Versions

![Matches per Edition](images/matches_per_edition.png)

- **What it shows**: Total matches played per tournament edition.
- **Key takeaway**: A clear step-function pattern — 17–38 matches (1930–1978), 52 matches (1982–1994), 64 matches (1998–2022, stable ever since).
- **Insight**: This chart, read alongside 4.6, is what reveals the 1994 anomaly — fewer matches did not mean fewer fans per match.
- **Suggested improved title**: *"Tournament Expansion: From 18 to 64 Matches Per World Cup"*

### 🌍 4.8 Number of Times Each Country Has Hosted the World Cup

![Hosting Frequency](images/hosting_frequency.png)

- **What it shows**: A count of hosting appearances by nation.
- **Key takeaway**: Only five nations — Brazil, Mexico, Germany, Italy, and France — have hosted twice; all others (17 nations) have hosted once.
- **Insight**: FIFA's rotation policy and the enormous infrastructure investment required for hosting keep repeat-hosting rare.
- **Suggested improved title**: *"Hosting Rights: A Short List of Repeat World Cup Hosts"*

### 🔝 4.9 Top 10 & 🔻 Bottom 10 Ranked Teams (FIFA Rankings, Oct 2022)

![Top and Bottom 10 FIFA Rankings](images/top_bottom_10_rankings.png)

- **What it shows**: Two horizontal bar charts — the 10 highest-ranked teams (Brazil down to Denmark) and the 10 lowest-ranked (San Marino up to Bahamas).
- **Key takeaway**: The top 10 reads like a "usual suspects" list of football powerhouses; the bottom 10 is composed of micro-nations and territories with minimal football infrastructure (San Marino, Anguilla, British/US Virgin Islands).
- **Insight**: The 200+ rank gap between #1 (Brazil, 1841.3 pts) and #211 (San Marino, 762.22 pts) illustrates just how wide the global competitive spectrum really is.
- **Suggested improved title**: *"Football's Two Extremes: FIFA's Elite Ten vs. the Final Ten"*

### 🥧 4.10 Team Rank Changes (Pie Chart)

![Rank Change Distribution](images/rank_change_pie.png)

- **What it shows**: Proportion of teams whose FIFA ranking rose, fell, or stayed the same versus the previous update.
- **Key takeaway**: 36.5% of teams (77) improved their rank, 32.2% (68) dropped, and 31.3% (66) were unchanged.
- **Insight**: Nearly 70% of the global rankings shifted in a single update cycle — the FIFA ranking system is highly dynamic, not a static leaderboard.
- **Suggested improved title**: *"The Ranking Shuffle: More Movers Than Stayers"*

### 🌎 4.11 Distribution of Teams by Association (Confederation)

![Teams by Confederation](images/teams_by_association.png)

- **What it shows**: Count of ranked national teams grouped by continental confederation (UEFA, CAF, AFC, CONCACAF, CONMEBOL, OFC).
- **Key takeaway**: UEFA, CAF, and AFC each field the largest number of member associations, while CONMEBOL (South America) has by far the fewest (only 10) — a reflection of the continent's small number of countries, not its footballing quality.
- **Insight**: This chart is an important reminder that **CONMEBOL's outsized World Cup success (Brazil, Argentina, Uruguay) comes from just 10 nations**, making it statistically the most "efficient" confederation per capita of member states.
- **Suggested improved title**: *"Quality Over Quantity: CONMEBOL's 10 Nations vs. the World"*

### 🧮 4.12 Percentage of Missing Values (Matches Dataset)

![Missing Values Heatmap-Style Bar Chart](images/missing_values_chart.png)

- **What it shows**: Percentage missing per column across the 44 original match-level fields.
- **Key takeaway**: Advanced metrics (xG, penalty shootout detail, red/yellow-red cards) are missing in 80–95%+ of rows, while core scoreline fields have 0% missingness.
- **Insight**: This is a textbook illustration of **survivorship bias in sports data collection** — richer statistical tracking only became standard in the 21st century.
- **Suggested improved title**: *"Data Through the Decades: Why Early World Cups Lack Modern Stats"*

### 🥅 4.13 Team Match-Volume & Scoring Charts (Top/Bottom 10 series)

![Match Volume and Scoring Charts](images/match_volume_scoring.png)

This group of charts (most matches played, fewest matches played, top/bottom home scorers, top/bottom away scorers, top/bottom goals conceded) collectively tells a **volume-adjusted performance story**:

- **What it shows**: Six paired bar charts contrasting the most active/prolific nations against the least active/lowest-scoring nations.
- **Key takeaway**: Brazil, Argentina, and Italy dominate nearly every "most" category simply by virtue of playing the most matches, while one-off qualifiers (Dutch East Indies, Zaire, Iceland's early appearances) anchor the "least" categories.
- **Insight**: Any team-level total (goals, matches, concessions) should ideally be **normalized per match** to enable fair cross-era comparison — a natural next step in this analysis (see Section 7).
- **Suggested improved title**: *"Volume vs. Value: Reading World Cup Totals in Context"*

---

## 5. Advanced Analysis & Statistical Insights

- **Rank Volatility Metric**: The 36.5% / 32.2% / 31.3% split (up / down / unchanged) derived from the FIFA ranking dataset is a simple but effective volatility indicator — it could be extended into a "ranking stability index" per confederation to see which regions have the most turnover.
- **Points-to-Rank Spread**: With a maximum of 1,841.30 points (Brazil) against an average of 1,220.69, elite teams sit roughly **51% above the global mean** — a useful benchmark for defining what statistically constitutes "elite" status in the FIFA points system.
- **Attendance Normalization**: By comparing total attendance (4.5) against average attendance (4.6), the notebook effectively performed an implicit normalization exercise that surfaced the 1994 anomaly — a strong example of why per-unit metrics often reveal more than aggregate totals.
- **Data Completeness Filtering**: The programmatic removal of columns exceeding 50% missingness (`if null_counts > 50: drop`) is a clean, reproducible data-hygiene pattern applicable to any long-horizon historical sports dataset.

> **🔑 Key Takeaway**: The most valuable analytical moves in this notebook weren't the raw counts themselves, but the **comparisons between related metrics** (matches vs. attendance, titles vs. finals reached, confederation size vs. World Cup success) — these juxtapositions are where the real insight emerged.

---

## 6. Conclusions & Recommendations

### ✅ Conclusions

1. **Brazil remains the sport's benchmark franchise** across nearly every dimension measured — titles, finals, matches played, and home goals scored.
2. **The World Cup's format expansion (16 → 24 → 32 teams)** has directly driven growth in total attendance and match count, but **per-match attendance is not purely a function of scale** — host-country infrastructure and market size (as seen in USA 1994) can outweigh raw match volume.
3. **The FIFA ranking system is highly dynamic**, with more than two-thirds of teams shifting position in a single ranking cycle, reinforcing that current form matters as much as historical pedigree.
4. **Historical scoring records (Fontaine, Kocsis) are effectively unbreakable** under the modern tournament structure, given fewer total matches per player and more sophisticated defensive systems.

### 💡 Recommendations

- For **sports broadcasters/marketers**: The 1994 USA attendance anomaly suggests future host selection in large, football-hungry but non-traditional markets can still generate record per-match engagement — a data point worth revisiting for future hosting bids.
- For **football analysts**: Normalize team performance metrics (goals, wins, matches) on a **per-tournament-appearance basis** rather than career totals, to enable fairer comparisons between nations with vastly different numbers of World Cup appearances.
- For **federation strategists**: CONMEBOL's disproportionate success relative to its small membership size (10 nations) is worth deeper investigation as a possible development-pathway benchmark for other confederations.

---

## 7. Limitations & Future Work

> ⚠️ **Known Limitations**

- **Missing advanced metrics** (xG, detailed penalty/card data) for pre-2000s matches limit the ability to perform consistent tactical or expected-goals analysis across the full 92-year history.
- **Raw totals are not appearance-normalized** — teams with more World Cup appearances will naturally lead most "total" charts (matches, goals, concessions) regardless of relative quality.
- **The FIFA ranking dataset is a single-day snapshot** (October 6, 2022) and does not capture ranking trends over time, limiting longitudinal ranking-trend analysis.
- **Country name inconsistencies** (e.g., "West Germany" vs. "Germany") slightly fragment historical team performance totals and would benefit from standardization for cleaner aggregate reporting.

> 🔮 **Suggested Future Work**

- Build a **per-appearance normalized leaderboard** (goals per match, wins per tournament entered) to complement the raw totals presented here.
- Merge the ranking snapshot with **multiple historical ranking pulls** to build a true time-series view of national team trajectory.
- Standardize historical nation names (West Germany → Germany, etc.) to produce a single unified "all-time Germany" performance record.
- Incorporate **knockout-stage-specific analysis** (Round of 16 onward) to isolate high-pressure performance from group-stage form.

---

## 8. Appendix

### 📎 8.1 Data Dictionary (Selected Key Fields)

| Column | Dataset | Description |
|---|---|---|
| `Year` | Champions / Matches | World Cup edition year |
| `Host` | Champions / Matches | Hosting nation |
| `Champion` / `Runner-Up` | Champions | Final match result |
| `TopScorrer` | Champions | Top scorer name(s) and goal count |
| `Attendance` / `AttendanceAvg` | Champions | Total and per-match average attendance |
| `rank` / `previous_rank` | Ranking | Current and prior FIFA ranking position |
| `points` / `previous_points` | Ranking | Current and prior FIFA ranking points |
| `home_team` / `away_team` | Matches | Competing nations |
| `home_score` / `away_score` | Matches | Final scoreline |

### 🧩 8.2 Representative Code Pattern (Column Cleanup)

```python
# Drop columns with more than 50% missing values
for column in matches.columns:
    null_counts = (matches[column].isnull().sum() / len(matches) * 100)
    if null_counts > 50:
        matches.drop(column, axis=1, inplace=True)
```

### 🧩 8.3 Representative Code Pattern (Top Scorer Parsing)

```python
# Extract goal count and clean player name from combined field
top_scorer_info = champions['TopScorrer'].str.split()
champions['num_goal_of_top_scorers'] = top_scorer_info.str[-1].astype(int)
champions['TopScorrer'] = champions['TopScorrer'].str.split(' - ').str[0]
```

---

<div align="center">

### 🏁 End of Report

*Prepared as a professional Markdown restructuring of an exploratory Jupyter Notebook analysis on FIFA World Cup history (1930–2022).*

⚽ **Data tells the story. Football writes the legend.** ⚽

</div>
