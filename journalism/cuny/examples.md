# Sourcetable Demo Brief — Journalism Students

A blow-by-blow guide for four separate scenarios, each covering a different beat. Each scenario includes a data source with direct URL, step-by-step Sourcetable actions, and AI prompts to type live.

---

## How to use this brief

- Each scenario is self-contained. Run one or all four.
- Type AI prompts **live and slowly** — the audience needs to see what you're asking.
- End every scenario by reading the sample headline out loud, then ask: *"Could you have written that without looking at the data?"*
- For a 15-minute demo: use Scenario 1 (Politics). For 45 minutes: use Scenario 3 (Environment) including the join step.

---

## Scenario 1 — Politics / Campaign Finance

**Premise:** Show who is funding a US congressman and whether the money tracks their voting record.

### Data source

**FEC PAC-to-Candidate contributions (direct CSV, no sign-up)**
https://www.fec.gov/data/browse-data/?tab=bulk-data

Download: `pas2` file under "Contributions from committees to candidates". It contains donor name, industry sector, dollar amount, recipient, state, and cycle year. Several thousand rows. No cleaning required.

**Backup / richer industry tagging:**
https://www.opensecrets.org/bulk-data

### Step-by-step in Sourcetable

1. Import the CSV. Point out that Sourcetable has auto-detected column types — amounts as numbers, dates as dates.
2. Filter the `recipient_state` column to a single state your audience will recognise.
3. Group by `industry` → SUM of `transaction_amt` → sort descending. You now have a ranked donor-industry table.
4. Build a bar chart: top 10 industries by total contribution. Title it with the candidate name.
5. Add a second filter: `transaction_amt > 50000`. Show how the donor list shrinks to the biggest players.
6. Type AI prompt 1 (below). Read the answer aloud.
7. Type AI prompt 2. Use the output as a "story memo" slide.

### AI prompts to type live

**Prompt 1 — top line finding**
> "Which industry gave the most money to this candidate, and how does it compare to the party average for that industry?"

**Prompt 2 — story angles**
> "Based on this contribution data, suggest three story angles a political reporter could follow up on. Be specific about what records or interviews they should seek."

**Prompt 3 — nut graf**
> "Write a single nut-graf sentence summarising the most surprising finding in this table, in the style of a newspaper story."

### Sample headline to land on

*"Real estate and finance donated $2.3M to [Candidate] — more than any other sector, and double the party average for their state."*

---

## Scenario 2 — Crime / Public Safety

**Premise:** Investigate whether a city is getting safer, and whether the headline rate holds up once you adjust for population.

### Data source

**Chicago open data portal — crimes 2001 to present**
https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2

Export a filtered CSV: set date range to the last 10 years, filter by primary type = ASSAULT, ROBBERY, HOMICIDE. Aim for 20,000–50,000 rows.

**Alternative — Los Angeles:**
https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8

**For the per-capita join — US Census population estimates by city:**
https://www.census.gov/data/tables/time-series/demo/popest/2020s-total-cities-and-towns.html

### Step-by-step in Sourcetable

1. Import the crime CSV. Highlight the `date` column — show Sourcetable parsing it as a date automatically.
2. Group by year → COUNT of rows. A trend table appears immediately. Note whether it goes up or down.
3. Filter to violent crimes only (ASSAULT, ROBBERY, HOMICIDE) using the `primary_type` column. Re-run the group.
4. Build a line chart: incident count by year. Add a second series for property crime as a comparison.
5. Import the Census population CSV as a second sheet.
6. Join on city name / year → calculate a new column: `incidents_per_100k = (count / population) * 100000`.
7. Re-plot the line chart using the per-capita figure. Show how the trend can shift.

### AI prompts to type live

**Prompt 1 — trend read**
> "Has violent crime increased or decreased over the last five years in this dataset? Give me the percentage change and whether it is statistically meaningful."

**Prompt 2 — anomaly hunt**
> "Is there a year or month where violent crime spiked or dropped unusually? What external events might explain it?"

**Prompt 3 — per capita reality check**
> "Now that we have a per-100,000 rate, does the trend look different from the raw count? Explain the difference in plain language a general audience would understand."

### Sample headline to land on

*"Violent crime fell 18% in five years — but adjusted for population growth, the real drop is less than half that."*

---

## Scenario 3 — Environment / Health

**Premise:** Find out whether air quality is worse in poorer counties, and build an environmental justice story from a two-dataset join.

### Data source

**EPA Air Quality System — annual AQI by county (direct download, no sign-up)**
https://aqs.epa.gov/aqsweb/airdata/download_files.html

Download: `annual_aqi_by_county_[most recent year].zip`. Unzip to get a clean CSV with columns for county, state, days good, days unhealthy, max AQI, and median AQI. Around 800 rows — perfect demo size.

**County Health Rankings — income, poverty, health outcomes by county:**
https://www.countyhealthrankings.org/health-data/methodology-and-sources/data-documentation

Download the national data CSV. It includes median household income, poverty rate, and health outcome scores keyed by county FIPS code.

**Bonus — EPA EJScreen for environmental justice angle:**
https://ejscreen.epa.gov/mapper/

### Step-by-step in Sourcetable

1. Import the EPA AQI CSV. Sort by `days_unhealthy` descending. The worst-air counties surface immediately — read them out.
2. Filter to a single state. Now you have a local story.
3. Import the County Health Rankings CSV as a second sheet.
4. Join on county FIPS code. You now have air quality + income + poverty in one table.
5. Add a calculated column: sort counties into income quintiles.
6. Group by income quintile → AVERAGE days unhealthy. Show whether low-income counties cluster at the unhealthy end.
7. Build a scatter plot: median household income (x-axis) vs days unhealthy (y-axis). The pattern should be visible.

### AI prompts to type live

**Prompt 1 — correlation**
> "Is there a pattern between median household income and days of unhealthy air quality across these counties? Describe what you see and how strong the relationship appears."

**Prompt 2 — worst-case profile**
> "Which five counties have the most unhealthy air days? What do they have in common — geography, industry, income level?"

**Prompt 3 — equity frame**
> "Frame this data as an environmental justice story. What is the central finding, which communities are most affected, and what is the strongest single statistic to lead with?"

### Sample headline to land on

*"Eight of the ten counties with the worst air quality fall below the state median income — in [State], pollution tracks poverty."*

---

## Scenario 4 — Education / Inequality

**Premise:** Investigate whether school funding gaps translate into outcome gaps, and find the districts that are being left behind.

### Data source

**Urban Institute Education Data Explorer — school-level spending and outcomes (filtered CSV download):**
https://educationdata.urban.org/data-explorer/schools

Filter to one state, select variables: per-pupil expenditure, free/reduced lunch eligibility (poverty proxy), enrolment, and reading/maths proficiency rate. Download as CSV. Typically 500–2,000 rows per state.

**Alternative — NCES Common Core of Data:**
https://nces.ed.gov/ccd/files.asp

**Alternative — Ed-Data.us (spending + outcomes by district, very clean):**
https://www.eddata.us/

### Step-by-step in Sourcetable

1. Import the school-level CSV. Point out the `free_lunch_pct` column as a poverty proxy.
2. Sort by `per_pupil_expenditure` descending. Read the highest and lowest figures aloud — the range is usually shocking.
3. Group by district → AVERAGE per-pupil spend, AVERAGE proficiency rate.
4. Build a scatter plot: per-pupil spend (x) vs proficiency rate (y).
5. Add colour encoding by free-lunch quintile. The clusters should separate visually.
6. Filter to the lowest-spending quartile. How many students does this represent?
7. Type AI prompt 3 — use the output as a closing "questions for the school board" slide.

### AI prompts to type live

**Prompt 1 — gap size**
> "What is the per-pupil spending gap between the highest and lowest funded quartile of schools, and is there a corresponding gap in proficiency rates?"

**Prompt 2 — outlier hunt**
> "Are there high-poverty schools that outperform their funding level? What might explain why they beat the trend?"

**Prompt 3 — accountability questions**
> "Based on this data, write three specific questions a reporter should put to the school board or district superintendent. Make them hard to deflect with a non-answer."

### Sample headline to land on

*"The poorest quarter of schools receive $3,400 less per student per year — and score 22 points lower on state proficiency tests."*

---

## Quick-reference: all data sources

| Category | Source | URL |
|---|---|---|
| **Politics** | FEC bulk data | https://www.fec.gov/data/browse-data/?tab=bulk-data |
| Politics | OpenSecrets bulk data | https://www.opensecrets.org/bulk-data |
| Politics | US Election 2020 Tweets (Kaggle) | https://www.kaggle.com/datasets/manchunhui/us-election-2020-tweets |
| Politics | US Presidential Donations (Kaggle) | https://www.kaggle.com/datasets/danerbland/electionfinance |
| Politics | Political fact-checking (HuggingFace) | https://huggingface.co/datasets/liar |
| Politics | Hate speech detection (HuggingFace) | https://huggingface.co/datasets/hate_speech_offensive |
| Politics | Tweet sentiment analysis (HuggingFace) | https://huggingface.co/datasets/tweet_eval |
| **Crime** | Chicago open data | https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-Present/ijzp-q8t2 |
| Crime | LA open data | https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8 |
| Crime | Census population estimates | https://www.census.gov/data/tables/time-series/demo/popest/2020s-total-cities-and-towns.html |
| Crime | US Police Shootings (Kaggle) | https://www.kaggle.com/datasets/ahsen1330/us-police-shootings |
| Crime | Global Terrorism Database (Kaggle) | https://www.kaggle.com/datasets/START-UMD/gtd |
| **Environment** | EPA AQI by county | https://aqs.epa.gov/aqsweb/airdata/download_files.html |
| Environment | County Health Rankings | https://www.countyhealthrankings.org/health-data/methodology-and-sources/data-documentation |
| Environment | EPA EJScreen | https://ejscreen.epa.gov/mapper/ |
| Environment | Climate Change Temperature (Kaggle) | https://www.kaggle.com/datasets/berkeleyearth/climate-change-earth-surface-temperature-data |
| Environment | Global Air Pollution (Kaggle) | https://www.kaggle.com/datasets/hasibalmuzdadid/global-air-pollution-dataset |
| **Education** | Urban Institute explorer | https://educationdata.urban.org/data-explorer/schools |
| Education | NCES Common Core | https://nces.ed.gov/ccd/files.asp |
| Education | Ed-Data.us | https://www.eddata.us/ |
| **Health** | COVID-19 Vaccination Progress (Kaggle) | https://www.kaggle.com/datasets/gpreda/covid-world-vaccination-progress |
| Health | US Healthcare Data (Kaggle) | https://www.kaggle.com/datasets/maheshdadhich/us-healthcare-data |
| **Economic** | World Happiness Report (Kaggle) | https://www.kaggle.com/datasets/unsdsn/world-happiness |
| Economic | Income Statistics by State (Kaggle) | https://www.kaggle.com/datasets/goldenoakresearch/us-household-income-stats-geo-locations |
| **News/Media** | CNN/DailyMail articles (HuggingFace) | https://huggingface.co/datasets/cnn_dailymail |
| News/Media | AG News - 120k articles (HuggingFace) | https://huggingface.co/datasets/ag_news |
| News/Media | 20 Newsgroups (HuggingFace) | https://huggingface.co/datasets/newsgroup |
| **Financial** | Financial news sentiment (HuggingFace) | https://huggingface.co/datasets/financial_phrasebank |