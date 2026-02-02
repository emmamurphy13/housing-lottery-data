Can you tell me something interesting from the housing lottery data

## Quick interesting insight 🔎

- **Dataset scale is telling:** lottery-applications.csv is a Git LFS pointer for a ~**892 MB** file — that implies **tens-to-hundreds of thousands of applications**, so competition per lottery is likely very high (big oversubscription). ✅  
- **Few lotteries, many applicants:** housing-lotteries.csv is small (~**296 KB**), suggesting **relatively few lottery records** (hundreds at most) but *many* applicants per lottery — a classic high‑demand, low‑supply scenario. ⚠️  
- **Implication:** With such volume, **priority rules (local, senior, disabled, income bands, set‑asides)** will materially change who gets housed — even small set‑asides can shift success rates a lot. 💡

What are some data visualizations that could be used with thos

## Visualizations to use with the housing‑lottery data 🔧📊

Here are focused, useful charts (short description + what to look for and suggested filters):

1. **Acceptance rate per lottery** — *Bar chart*  
   - Shows % of applicants who were offered/accepted per development.  
   - Look for very low rates and outliers.  
   - Filters: neighborhood, income band, date range.

2. **Oversubscription distribution** — *Histogram / density*  
   - Applicants per unit (applicants ÷ units_offered).  
   - Reveals how intense competition is and tail behavior.  
   - Filters: unit type, neighborhood.

3. **Success rate by priority group** — *Bar chart with error bars*  
   - Compares acceptance probabilities for `local`, `senior`, `disabled`, `none`.  
   - Highlights policy impact (set‑asides).  
   - Drilldowns: by lottery, income band.

4. **Applicants by income / household size** — *Violin or boxplot*  
   - Distribution of incomes and household sizes among applicants.  
   - Check for income thresholds and crowding trends.

5. **Map of demand vs supply** — *Choropleth / sized points on a map*  
   - Neighborhoods colored by applicants per unit, or points sized by units_offered.  
   - Useful for geographic hot spots (needs `latitude/longitude` or neighborhood lookup).

6. **Timeline: applications & offers over time** — *Line chart / stacked area*  
   - Tracks application volume and offer events across months.  
   - Reveals seasonality or policy-driven spikes.

7. **Top oversubscribed lotteries** — *Sorted horizontal bar chart*  
   - Simple leaderboard of most competitive developments (apps per unit).

8. **Offer flow / outcome Sankey** — *Sankey diagram*  
   - Visualize flow from applicants → offers → accepted/declined → waitlist.

9. **Acceptance vs income scatter / regression** — *Scatterplot with LOESS*  
   - See whether lower incomes are prioritized or excluded (income vs probability of offer).

10. **Waitlist depth / time‑to‑offer** — *ECDF or histogram of days to offer*  
    - Measures how long people wait from application to receiving an offer.

11. **Composition treemap** — *Treemap by neighborhood & income band*  
    - Visual share of applicants and units by combination (compact visual for editorial pieces).

12. **Interactive dashboard** — *Filterable Plotly / Vega / Power BI dashboard*  
    - Combine several views, allow filters (neighborhood, set‑aside, income band, household size).

Can you rank this list from easiest to hardest to construct
## Ranked: easiest → hardest to construct 🔧📊

1. **Top oversubscribed lotteries — horizontal bar chart** ✅  
   - Simple count per lottery; minimal aggregation. Tools: Seaborn/Matplotlib, Plotly.

2. **Oversubscription distribution — histogram / density** ✅  
   - Single numeric column (apps/units); trivial plot.

3. **Acceptance rate per lottery — bar chart** ✅  
   - Requires join/aggregation (accepted ÷ applicants), but straightforward.

4. **Success rate by priority group — bar chart (+ error bars)** ✅  
   - Group-by + proportion; add CI if desired (bootstraps or statsmodels).

5. **Applicants by income / household size — violin / boxplot** ⚖️  
   - Needs cleaning/outlier handling, but standard.

6. **Composition treemap (neighborhood × income band)** ⚖️  
   - Aggregate counts; needs a treemap library (squarify, Plotly).

7. **Acceptance vs income scatter + regression/LOESS** ⚠️  
   - Point plot + smoothing/regression; watch for heteroskedasticity and bins.

8. **Timeline: applications & offers over time — line / stacked area** ⚠️  
   - Date parsing, resampling, stacked series; more data prep.

9. **Waitlist depth / time-to-offer — ECDF / histogram** ⚠️  
   - Requires dates for application → offer and handling censored/waiting cases.

10. **Map of demand vs supply — choropleth / sized points** 🔧  
    - Needs geocoding or shapefiles and spatial joins (Folium, Kepler, GeoPandas).

11. **Offer flow / outcome Sankey** 🔧  
    - Build aggregated flow table (applicant → offer → accepted/declined → waitlist); needs a Sankey lib (Plotly).

12. **Interactive dashboard (filterable, multi-view)** 🚧  
    - Highest effort: UI, cross-filtering, state management (Dash/Panel/Streamlit/Observable), performance tuning.

    Why should I investigate this data set
    ## Why investigate this dataset? 🔎✨

- **Public-interest impact** — It measures how well scarce affordable housing is being allocated; findings can influence policy and public opinion. ✅  
- **Quantifiable accountability** — You can show who *actually* gets offers (vs. who’s eligible), revealing whether rules and set‑asides work as intended. 📊  
- **Unearth inequities** — Detect disparities by income, household size, priority group, or neighborhood. This is a strong basis for reporting or policy recommendations. ⚖️  
- **Storytelling potential** — Big, simple metrics (acceptance rates, wait times, oversubscription leaders) make clear, human‑centered narratives for readers. 🗞️  
- **Operational insight** — Cities and non‑profits can use it to adjust targeting, outreach, and unit mixes. 🔧  
- **Reproducibility & trust** — Data-backed claims + shared code/notebooks build credibility for newsroom investigations.

---

## Key questions to answer first 🧭
- What’s the overall acceptance rate and median wait time?  
- Which lotteries are most oversubscribed (apps per unit)?  
- Do priority groups (local, seniors, disabled) actually have higher success rates?  
- Are certain neighborhoods or income bands underserved?  
- Are there data quality issues (duplicates, missing incomes, inconsistent IDs)?

---

## Quick analyses / visualizations to run (first pass) 📈
1. Acceptance rate per lottery (bar)  
2. Oversubscription distribution (histogram)  
3. Success rate by priority group (bar with CI)  
4. Map: applicants per unit by neighborhood (choropleth/points)  
5. Time‑to‑offer distribution (ECDF / histogram)  
6. Top oversubscribed lotteries (horizontal bar)
