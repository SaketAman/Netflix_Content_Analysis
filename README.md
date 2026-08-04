<img width="1166" height="656" alt="Screenshot 2026-08-04 121913" src="https://github.com/user-attachments/assets/321e0aaa-865d-43dd-bfb9-d51b62bec30c" />


# Netflix Content Analysis Dashboard

## Overview
This dashboard visualizes Netflix's content catalog — 5,837 verified titles spanning Movies and TV Shows — covering content mix, genre performance, revenue, ratings, geographic reach, and catalog growth over time. It was built on top of a cleaned and validated version of the raw `NETFLIX_DATASET.xlsx` source file.

**Live metrics at a glance:**
| KPI | Value |
|---|---|
| Total Revenue (USD millions) | 45.91K |
| Total Shows | 5.837K |
| Country of release | 72 |
| Average Rating | 6.51 |

---

## Data Source & Preparation
The dashboard is built on the **cleaned** version of the dataset, not the raw file. Before this data was loaded, the following issues were identified and resolved — see `Netflix_Cleaned_Analysis.xlsx` for the full audit trail:

| Issue | Resolution |
|---|---|
| Duplicate sheet with corrupted title casing | Discarded; used the properly cased "Raw Data" sheet as the single source of truth |
| 100 fabricated/synthetic rows (recycled name pools, duplicate titles, future release years) | Identified and excluded from analysis |
| Garbled accented characters (mojibake) in title/director/cast/description | Re-decoded and fixed (224 directors, 108 titles, 822 cast entries, 138 descriptions) |
| Inconsistent whitespace | Trimmed across all text fields |
| Unstructured `duration` and `date_added` fields | Parsed into numeric minutes/seasons and proper date types |
| Missing values (director 32.6%, cast 9.5%, country 7.3%, date_added 11%) | Left blank rather than imputed, to avoid misleading the visuals |

**Final dataset used for this dashboard:** 5,837 rows × 19 columns.

---

## Dashboard Components

### Header
- **Netflix branding** and title banner.
- **Netflix_availability** dropdown slicer — filters the entire dashboard by *Available*, *Removed*, or *Leaving Soon*.
- **Type** checkboxes — filters by *Movie* / *TV Show*.

### KPI Cards
Four headline cards summarizing the filtered selection:
- **Total Revenue (USD millions)** — sum of `box_revenue` (Movies only; TV Shows have no box revenue by design).
- **Total Shows** — count of titles in the current filter context.
- **Country of release** — distinct count of primary country of release across all titles: 71 identified countries plus 1 "Unknown" bucket for titles with no country data (72 total).
- **Average Rating** — mean IMDb rating across the filtered titles.

### Genre Table
Left-hand table listing all 14 genres with total title counts (Drama and Comedy lead the catalog), sortable and clickable to cross-filter the rest of the dashboard.

### Avg Revenue ($M) by Genre
Bar chart ranking genres by average box revenue per movie. Sci-Fi & Fantasy and Music titles command the highest average revenue despite lower title counts — a niche-but-lucrative pattern.

### Country Map
Bing Maps visual plotting title concentration by country; density is heaviest across North America, Western Europe, and South Asia, consistent with the United States (39.6% share) and India leading the catalog.

### Top 10 Directors by Shows
Horizontal bar chart of the most prolific directors by title count, led by Raúl Campos & Jan Suter, Marcus Raboy, and Jay Karas.

### Shows Added by Year
Area chart tracking catalog growth by `date_added` year — shows a steep ramp from 2015 onward, peaking around 2019, reflecting Netflix's major content investment period.

### Total Shows by Country
Donut chart breaking down title share by country: United States (49.7%), India (16.88%), United Kingdom, Canada, Japan, South Korea, and others.

---

## Key Insights
- **Movies dominate the catalog** at roughly 68% of titles vs. 32% TV Shows.
- **Drama and Comedy are the largest genres by volume**, but **Sci-Fi & Fantasy and Music generate the highest average revenue per title**.
- **The US and India together account for ~66% of all titles**, making them the dominant content markets.
- **Catalog growth was heavily front-loaded in 2015–2019** (69.4% of all titles were released in this window), with additions tapering off sharply after 2019.
- **Average IMDb rating sits at 6.51**, with only ~10% of titles rated 8+ — the catalog skews toward broadly-appealing, mid-rated content rather than critically acclaimed outliers.

---

## How to Use
1. Use the **Netflix_availability** slicer to focus on currently available content, or investigate what's been removed/leaving.
2. Use the **Type** checkboxes to isolate Movie-only or TV Show-only trends (note: revenue and duration metrics behave differently by type).
3. Click any genre in the **Genre table** to cross-filter all other visuals to that genre.
4. Hover over the **Country map** or **donut chart** for exact counts and percentages per country.

## Known Limitations
- `box_revenue` and revenue-based visuals apply to Movies only — TV Shows have no comparable metric in this dataset.
- The **Country of release** figure of 72 includes an "Unknown" bucket for the 7.3% of titles with no country data; 71 countries have a confirmed release country.
- Director, cast, and country fields have meaningful missingness (see table above) — visuals built on these fields reflect only the titles with known values.

## Files
- Netfilx Dashboard.pbix — Power BI dashboard file consisting all the charts and KPIs.
- Netflix_Cleaned_Analysis.xlsx — original raw source file, cleaned dataset, synthetic-record audit, and summary tables/charts used to build this dashboard.
- Netfilx_Analytics_Presentation.pptx — This is the presentation file for better understanding.
