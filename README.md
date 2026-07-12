<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Righteous&size=38&duration=3000&pause=1000&color=2ECC71&center=true&vCenter=true&width=850&height=70&lines=FIFA+WORLD+CUP+DATA+ANALYSIS;92+YEARS+OF+FOOTBALL+HISTORY;22+EDITIONS+%C2%B7+964+MATCHES+%C2%B7+211+TEAMS;1930+%E2%86%92+2022" alt="Animated Title" />

<br>

<img src="https://img.shields.io/badge/⚽_Editions-22-2ECC71?style=for-the-badge&labelColor=0B3D24" />
<img src="https://img.shields.io/badge/🗓️_Span-1930--2022-F5B700?style=for-the-badge&labelColor=0A1128" />
<img src="https://img.shields.io/badge/📊_Matches-964-3AA0FF?style=for-the-badge&labelColor=0A1128" />
<img src="https://img.shields.io/badge/🌍_Teams-211-EF4444?style=for-the-badge&labelColor=0A1128" />
<img src="https://img.shields.io/badge/✅_Status-Complete-2ECC71?style=for-the-badge&labelColor=0B3D24" />

<br><br>

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=14&duration=2600&pause=900&color=F5B700&center=true&vCenter=true&width=760&height=30&lines=%F0%9F%8F%86+Brazil+%E2%80%94+5+titles%2C+7+finals;%E2%9A%A1+Just+Fontaine+%E2%80%94+13+goals+in+1958;%F0%9F%8E%9F%EF%B8%8F+USA+1994+%E2%80%94+highest+ever+avg.+attendance;%F0%9F%8C%8D+36.5%25+of+ranked+teams+rose+in+Oct+2022" alt="Ticker" />

</div>

---

> 📌 **About this report**: A professional restructuring and narrative expansion of a Jupyter Notebook that analyzed three FIFA World Cup datasets — historical champions (1930–2022), the October 2022 FIFA World Ranking, and match-level results spanning nine decades.

---

## 🧾 Executive Summary

<table>
<tr>
<td width="20%" align="center">🏆</td>
<td><b>Brazil is the undisputed king of the tournament</b> — the only nation with 5 titles, 7 final appearances, and the record for both most home goals scored and most matches played (103).</td>
</tr>
<tr>
<td align="center">⚡</td>
<td><b>Just Fontaine's 13-goal haul at the 1958 World Cup</b> remains the most goals scored by a single player in one edition — a record that has stood for over 65 years.</td>
</tr>
<tr>
<td align="center">📈</td>
<td><b>Tournament scale has grown four-fold</b> — from 18 matches in 1930 to a steady 64 matches per edition since 1998, reflecting expansion from 13–16 teams to 32.</td>
</tr>
<tr>
<td align="center">🇺🇸</td>
<td><b>1994 USA is the attendance outlier</b> — fewer matches (52) than every edition from 2002 onward (64), yet the <b>highest average attendance per match (68,991)</b> in history.</td>
</tr>
<tr>
<td align="center">🌍</td>
<td><b>FIFA rankings (Oct 2022) show real mobility</b> — 36.5% of 211 teams improved, 32.2% dropped, and only 31.3% held steady.</td>
</tr>
</table>

---

## 📚 Table of Contents

<div align="center">

[![Intro](https://img.shields.io/badge/1-Introduction-0D5C34?style=flat-square)](#1-introduction)
[![EDA](https://img.shields.io/badge/2-Data_%26_EDA-1F8F4F?style=flat-square)](#2-data-overview--exploratory-data-analysis-eda)
[![Findings](https://img.shields.io/badge/3-Key_Findings-2ECC71?style=flat-square)](#3-key-findings--insights)
[![Viz](https://img.shields.io/badge/4-Visualizations-F5B700?style=flat-square)](#4-visualizations-analysis)
[![Advanced](https://img.shields.io/badge/5-Advanced_Analysis-D99400?style=flat-square)](#5-advanced-analysis--statistical-insights)
[![Conclusions](https://img.shields.io/badge/6-Conclusions-3AA0FF?style=flat-square)](#6-conclusions--recommendations)
[![Limitations](https://img.shields.io/badge/7-Limitations-EF4444?style=flat-square)](#7-limitations--future-work)
[![Appendix](https://img.shields.io/badge/8-Appendix-0A1128?style=flat-square)](#8-appendix)

</div>

---

## 1. Introduction

<img src="https://img.shields.io/badge/SECTION-01-2ECC71?style=flat-square&labelColor=0A1128" />

### 🎯 Objective of the Analysis

The purpose of this analysis is to build a data-driven understanding of FIFA World Cup history by answering questions such as:

- Which nations and players have historically dominated the tournament?
- How has the World Cup evolved in scale (teams, matches, attendance) since 1930?
- What patterns exist in scoring, home/away performance, and defensive resilience?
- How does the current FIFA global ranking landscape (as of October 2022) compare to historical World Cup success?

The analysis blends **historical tournament records** with a **snapshot of current national team rankings** and **granular match-level statistics**, creating a 360° view of international football performance.

### 🗂️ Dataset Description

| Dataset | File | Rows | Key Columns | Time Span |
|---|---|---:|---|---|
| 🏆 World Cup Champions | `world_cup.csv` | 22 | Year, Host, Teams, Champion, Runner-Up, Top Scorer, Attendance, AttendanceAvg, Matches | 1930 – 2022 |
| 🌍 FIFA World Ranking | `fifa_ranking_2022-10-06.csv` | 211 | Team, Association, Rank, Previous Rank, Points, Previous Points | Snapshot: Oct 6, 2022 |
| ⚽ Match Results | `matches_1930_2022.csv` | 964 | Home/Away Team, Score, Managers, Captains, Attendance, Venue, Round, Referee, Goals, Cards | 1930 – 2022 |

> 💡 **Note:** Each of the 22 World Cup editions is represented once in the champions dataset, while the matches dataset captures **every individual match** ever played across all 22 editions — 964 matches in total.

---

## 2. Data Overview & Exploratory Data Analysis (EDA)

<img src="https://img.shields.io/badge/SECTION-02-1F8F4F?style=flat-square&labelColor=0A1128" />

### 🔍 Shape, Duplicates & Missing Values

<details>
<summary><strong>📊 Click to expand: Dataset-by-dataset EDA summary</strong></summary>

<br>

**Champions Dataset (`world_cup.csv`)**
- 22 rows × 8 original columns
- Top scorer field required parsing (e.g., `"Kylian Mbappé - 8"`) — split into player name and goal count via string operations
- No explicit missing-value or duplicate-check was needed given the dataset's small, curated size

**FIFA Ranking Dataset (`fifa_ranking_2022-10-06.csv`)**

![clean](https://img.shields.io/badge/Duplicates-0-2ECC71?style=flat-square) ![clean](https://img.shields.io/badge/Missing_Values-0-2ECC71?style=flat-square)

- 211 rows × 7 original columns (→ 6 after dropping the redundant `team_code` column)
- `team` and `rank` both contain exactly 211 unique values, confirming a one-to-one team-to-rank mapping

**Matches Dataset (`matches_1930_2022.csv`)**

![clean](https://img.shields.io/badge/Duplicates-0-2ECC71?style=flat-square) ![warn](https://img.shields.io/badge/Heavy_Missingness-xG_%26_Penalty_Fields-EF4444?style=flat-square)

- 964 rows × 44 original columns
- Significant missingness in advanced/modern metrics: `home_xg`, `away_xg`, `home_penalty`, `away_penalty`, and shootout/red-card detail fields were missing in **more than 50% of rows** — a direct consequence of expected-goals (xG) and detailed event tracking only being recorded in recent tournaments
- Columns exceeding the 50% missing-value threshold were **programmatically dropped**, reducing the working dataset to a leaner, higher-quality set of 25 columns

</details>

#### 📉 Missing Data Visualization

> The notebook produced a horizontal bar chart plotting the **percentage of missing values per column** in the matches dataset. Columns such as `home_xg`, `away_xg`, `home_penalty`, and `away_penalty` towered above the 80–95% missing mark, while core fields (`home_team`, `away_team`, `home_score`, `away_score`, `Date`, `Year`) showed **0% missingness**.

> ✅ **Data Quality Verdict**: All three datasets are duplicate-free. The ranking dataset is pristine (no nulls). The matches dataset requires selective column-pruning due to historical data-collection gaps — a completely expected pattern for a 92-year time series where modern analytics (xG, VAR-era penalty tracking) simply didn't exist for early tournaments.

### 📈 Statistical Summary (FIFA Ranking Points)

| Metric | Value | Team |
|---|---:|---|
| Maximum Points | **1,841.30** | 🇧🇷 Brazil |
| Minimum Points | **762.22** | 🇸🇲 San Marino |
| Average Points (211 teams) | **1,220.69** | — |

This ~1,079-point spread between #1 and #211 illustrates the steep competitive gradient in international football — Brazil's points total is roughly **2.4× higher** than San Marino's.

```
Brazil        ████████████████████████████████████████  1841.3
Global Avg     ███████████████████████████               1220.7
San Marino     ███████████                                762.2
```

---

## 3. Key Findings & Insights

<img src="https://img.shields.io/badge/SECTION-03-2ECC71?style=flat-square&labelColor=0A1128" />

### 🏆 Historical Performance of Top Teams

- **Brazil** leads all-time World Cup wins with a commanding margin, followed by **Italy**, then **Argentina** (whose 2022 Qatar triumph pushed them to third), with **Germany/West Germany**, **France**, and **Uruguay** rounding out the multi-time-champion tier.
- When **runner-up finishes** are added to titles, **Brazil (7 total final appearances)** still tops the list, but **Argentina and Italy (6 each)** and **West Germany (5)** show remarkable consistency in reaching football's biggest stage — even when they didn't lift the trophy.
- **Argentina, West Germany, and the Netherlands** share the unfortunate distinction of the most runner-up finishes (3 each) — the Netherlands notably has *never* won a World Cup despite three final appearances, making it the most successful "bridesmaid" nation in tournament history.

### ⚽ Goal Trends & Scoring Patterns

- The **Golden Boot leaderboard** is dominated by an interesting mix of eras: **Just Fontaine (13 goals, 1958)** and **Sándor Kocsis (11 goals, 1954)** from football's early "high-scoring" decades sit well above modern top scorers like **Ronaldo and Mbappé (8 goals each)**.
- **Gerd Müller (10 goals, 1970)** and **Eusébio (9 goals, 1966)** further reinforce that the 1950s–1970s were the golden age of prolific individual scoring at the World Cup.
- **Brazil is the top home-scoring nation** by a wide margin (~190 goals), nearly 60% more than second-placed Argentina.
- In **away scoring**, the gap narrows considerably: **Brazil, France, and Spain** are closely bunched near the top (~47–48 goals each).

### 🏟️ Tournament Scale & Attendance Analysis

- Match count per edition has grown in three distinct "eras":

```
1930–1978   ████████                17–38 matches (13–16 teams)
1982–1994   ████████████████        52 matches (24 teams)
1998–2022   ████████████████████    64 matches (32 teams, stable)
```

- Despite fewer matches, **1994 (USA)** recorded the tournament's **highest-ever average attendance per match (68,991)** — even surpassing every edition from 2002 to 2022.
- **Host nation analysis** shows only five countries have hosted twice: **Brazil, Mexico, Germany, Italy, and France** — every other host nation (17 countries) has hosted exactly once.

### 🏠 Home Advantage & Match-Level Analysis

- **Brazil has played more World Cup matches (103) than any other nation**, roughly 15 more than second-placed Argentina (88).
- At the opposite end, nations like **Dutch East Indies (1 match)**, **Zaire, Trinidad and Tobago, UAE, Qatar, and Iceland (3 matches each)** represent single-appearance or early-elimination stories.
- **Defensive resilience** tells a different story than attacking output: Brazil, Argentina, and Mexico also appear among the **most goals conceded**, a natural consequence of playing the most matches.
- Teams like **Angola, Israel, and Iraq** show the **fewest goals conceded**, largely because of their limited number of tournament appearances rather than superior defense.

> **🔑 Key Takeaway**: Team success at the World Cup is multidimensional — trophy counts, final appearances, goals scored, goals conceded, and matches played each tell a different part of the story. Brazil consistently leads on nearly every dimension, but the runner-up and scoring-trend data reveal deep nuance beneath the top-line titles table.

---

## 4. Visualizations Analysis

<img src="https://img.shields.io/badge/SECTION-04-F5B700?style=flat-square&labelColor=0A1128" />

Below is a structured breakdown of every major visualization produced in the source notebook, along with the insight each one delivers.

### 📊 4.1 Top Scorers and Their Goals

![Top Scorers and Their Goals](images/top_scorers_goals.png)

![What](https://img.shields.io/badge/WHAT-Chart_Shows-3AA0FF?style=flat-square) Every World Cup's top scorer plotted against their goal tally, ordered chronologically (2022 → 1930).

![Takeaway](https://img.shields.io/badge/KEY-Takeaway-D99400?style=flat-square) Just Fontaine's 13-goal 1958 campaign is a clear outlier at the top of the range; most modern top scorers cluster around 6–8 goals.

![Insight](https://img.shields.io/badge/SPORTS-Insight-0D5C34?style=flat-square) The chart visually confirms a *declining ceiling* for individual scoring, driven by tighter defensive tactics.

> 💬 Suggested improved title: *"Golden Boot Winners Across 22 World Cups: The Fontaine Anomaly"*

### 🏆 4.2 Teams with the Most World Cup Wins

![World Cup Wins by Team](images/wins_by_team.png)

A ranked bar chart of every World Cup–winning nation and their total title count. Brazil sits clearly above the pack, followed by Italy and Argentina, with a tightly bunched second tier (Germany, France, Uruguay, West Germany). Only **8 nations** have *ever* won the World Cup in 22 editions.

> 💬 Suggested improved title: *"The Exclusive Club: 8 Nations, 22 Titles"*

### 🥈 4.3 Teams with the Most Runner-Up Finishes

![Runner-Up Finishes](images/runner_up_finishes.png)

Nations ranked by number of World Cup final losses. Argentina, West Germany, and the Netherlands share the top spot with 3 runner-up finishes each. The Netherlands' presence — with **zero titles** — makes them the most notable "nearly team" in World Cup history.

> 💬 Suggested improved title: *"So Close: The Nations That Reached the Final Most, Without the Trophy"*

### 🎯 4.4 Teams with the Most World Cup Final Appearances

![Final Appearances](images/final_appearances.png)

Combined champion + runner-up appearances per nation. Brazil (7), Argentina and Italy (6 each), and West Germany (5) form the tournament's true "final four" of consistency.

> 💬 Suggested improved title: *"The Finalist Elite: Who Reaches the Big Match Most Often?"*

### 🎟️ 4.5 Total Attendance of FIFA World Cup Versions

![Total Attendance](images/total_attendance.png)

Aggregate tournament attendance by year, 1930–2022. Clear upward trend from under 600,000 total attendees in 1930 to well above 3 million from the 1990s onward.

> 💬 Suggested improved title: *"From Uruguay to Qatar: The Growth of World Cup Attendance"*

### 📐 4.6 Attendance Average of FIFA World Cup Versions

![Average Attendance](images/average_attendance.png)

Per-match average attendance by year. **1994 (USA) stands out dramatically**, with an average of ~68,991 attendees per match, the highest in tournament history.

> 💬 Suggested improved title: *"The 1994 Anomaly: Why the USA World Cup Still Holds the Attendance Record"*

### 🗓️ 4.7 Number of Matches in FIFA World Cup Versions

![Matches per Edition](images/matches_per_edition.png)

A clear step-function pattern — 17–38 matches (1930–1978), 52 matches (1982–1994), 64 matches (1998–2022, stable ever since).

> 💬 Suggested improved title: *"Tournament Expansion: From 18 to 64 Matches Per World Cup"*

### 🌍 4.8 Number of Times Each Country Has Hosted the World Cup

![Hosting Frequency](images/hosting_frequency.png)

Only five nations — Brazil, Mexico, Germany, Italy, and France — have hosted twice; all others (17 nations) have hosted once.

> 💬 Suggested improved title: *"Hosting Rights: A Short List of Repeat World Cup Hosts"*

### 🔝 4.9 Top 10 & 🔻 Bottom 10 Ranked Teams (FIFA Rankings, Oct 2022)

![Top and Bottom 10 FIFA Rankings](images/top_bottom_10_rankings.png)

The top 10 reads like a "usual suspects" list of football powerhouses; the bottom 10 is composed of micro-nations and territories with minimal football infrastructure.

> 💬 Suggested improved title: *"Football's Two Extremes: FIFA's Elite Ten vs. the Final Ten"*

### 🥧 4.10 Team Rank Changes

<div align="center">

![Up](https://progress-bar.dev/36/?title=📈%20Up%20(77%20teams)&width=400&color=2ecc71)
![Down](https://progress-bar.dev/32/?title=📉%20Down%20(68%20teams)&width=400&color=ef4444)
![Flat](https://progress-bar.dev/31/?title=➖%20Unchanged%20(66%20teams)&width=400&color=3aa0ff)

</div>

36.5% of teams (77) improved their rank, 32.2% (68) dropped, and 31.3% (66) were unchanged. Nearly 70% of the global rankings shifted in a single update cycle.

> 💬 Suggested improved title: *"The Ranking Shuffle: More Movers Than Stayers"*

### 🌎 4.11 Distribution of Teams by Association (Confederation)

![Teams by Confederation](images/teams_by_association.png)

UEFA, CAF, and AFC each field the largest number of member associations, while CONMEBOL (South America) has by far the fewest (only 10) — CONMEBOL's outsized World Cup success from just 10 nations makes it statistically the most "efficient" confederation per capita of member states.

> 💬 Suggested improved title: *"Quality Over Quantity: CONMEBOL's 10 Nations vs. the World"*

### 🧮 4.12 Percentage of Missing Values (Matches Dataset)

![Missing Values Chart](images/missing_values_chart.png)

Advanced metrics (xG, penalty shootout detail, cards) are missing in 80–95%+ of rows, while core scoreline fields have 0% missingness — a textbook illustration of survivorship bias in sports data collection.

> 💬 Suggested improved title: *"Data Through the Decades: Why Early World Cups Lack Modern Stats"*

### 🥅 4.13 Team Match-Volume & Scoring Charts (Top/Bottom 10 series)

![Match Volume and Scoring Charts](images/match_volume_scoring.png)

Six paired bar charts contrasting the most active/prolific nations against the least active/lowest-scoring nations. Brazil, Argentina, and Italy dominate nearly every "most" category simply by virtue of playing the most matches.

> 💬 Suggested improved title: *"Volume vs. Value: Reading World Cup Totals in Context"*

---

## 5. Advanced Analysis & Statistical Insights

<img src="https://img.shields.io/badge/SECTION-05-D99400?style=flat-square&labelColor=0A1128" />

- **Rank Volatility Metric**: The 36.5% / 32.2% / 31.3% split (up / down / unchanged) is a simple but effective volatility indicator — extendable into a "ranking stability index" per confederation.
- **Points-to-Rank Spread**: With a maximum of 1,841.30 points (Brazil) against an average of 1,220.69, elite teams sit roughly **51% above the global mean**.
- **Attendance Normalization**: Comparing total attendance against average attendance surfaced the 1994 anomaly — a strong example of why per-unit metrics often reveal more than aggregate totals.
- **Data Completeness Filtering**: The programmatic removal of columns exceeding 50% missingness is a clean, reproducible data-hygiene pattern applicable to any long-horizon historical sports dataset.

> **🔑 Key Takeaway**: The most valuable analytical moves in this notebook weren't the raw counts themselves, but the **comparisons between related metrics** — these juxtapositions are where the real insight emerged.

---

## 6. Conclusions & Recommendations

<img src="https://img.shields.io/badge/SECTION-06-3AA0FF?style=flat-square&labelColor=0A1128" />

### ✅ Conclusions

1. **Brazil remains the sport's benchmark franchise** across nearly every dimension measured — titles, finals, matches played, and home goals scored.
2. **The World Cup's format expansion** has directly driven growth in total attendance and match count, but **per-match attendance is not purely a function of scale**.
3. **The FIFA ranking system is highly dynamic**, with more than two-thirds of teams shifting position in a single ranking cycle.
4. **Historical scoring records (Fontaine, Kocsis) are effectively unbreakable** under the modern tournament structure.

### 💡 Recommendations

- For **sports broadcasters/marketers**: The 1994 USA attendance anomaly suggests future host selection in large, football-hungry but non-traditional markets can still generate record per-match engagement.
- For **football analysts**: Normalize team performance metrics on a **per-tournament-appearance basis** rather than career totals.
- For **federation strategists**: CONMEBOL's disproportionate success relative to its small membership size is worth deeper investigation as a possible development-pathway benchmark.

---

## 7. Limitations & Future Work

<img src="https://img.shields.io/badge/SECTION-07-EF4444?style=flat-square&labelColor=0A1128" />

> ⚠️ **Known Limitations**

- **Missing advanced metrics** (xG, detailed penalty/card data) for pre-2000s matches limit tactical analysis across the full 92-year history.
- **Raw totals are not appearance-normalized** — teams with more World Cup appearances naturally lead most "total" charts.
- **The FIFA ranking dataset is a single-day snapshot** (October 6, 2022), limiting longitudinal ranking-trend analysis.
- **Country name inconsistencies** (e.g., "West Germany" vs. "Germany") slightly fragment historical performance totals.

> 🔮 **Suggested Future Work**

- Build a **per-appearance normalized leaderboard** (goals per match, wins per tournament entered).
- Merge the ranking snapshot with **multiple historical ranking pulls** to build a true time-series view.
- Standardize historical nation names to produce a single unified "all-time Germany" performance record.
- Incorporate **knockout-stage-specific analysis** to isolate high-pressure performance from group-stage form.

---

## 8. Appendix

<img src="https://img.shields.io/badge/SECTION-08-0A1128?style=flat-square&labelColor=2ECC71" />

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

<img src="https://readme-typing-svg.demolab.com?font=Righteous&size=26&duration=3200&pause=1000&color=F5B700&center=true&vCenter=true&width=600&height=45&lines=END+OF+REPORT;THANK+YOU+FOR+READING" alt="End Banner" />

<br>

<img src="https://img.shields.io/badge/⚽_22_Editions-2ECC71?style=for-the-badge&labelColor=0B3D24" />
<img src="https://img.shields.io/badge/🏆_8_Champion_Nations-F5B700?style=for-the-badge&labelColor=0A1128" />
<img src="https://img.shields.io/badge/📊_964_Matches-3AA0FF?style=for-the-badge&labelColor=0A1128" />
<img src="https://img.shields.io/badge/🌍_211_Teams-EF4444?style=for-the-badge&labelColor=0A1128" />

<br><br>

*Prepared as a professional Markdown restructuring of an exploratory Jupyter Notebook analysis on FIFA World Cup history (1930–2022).*

**⚽ Data tells the story. Football writes the legend. ⚽**

</div>
