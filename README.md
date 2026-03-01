#  Airline Delay Data Pipeline

An end-to-end ETL pipeline and exploratory analysis of U.S. airline delay data, built in a Jupyter Notebook using Python, pandas, and seaborn.

> **Dataset:** [Airline Delay – Kaggle](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data)

---

## Overview

This project loads raw airline delay data, cleans and transforms it, engineers new features, and produces a set of visualizations to surface patterns in flight delays across carriers, months, and delay types.

---

## Pipeline Steps

### Step 1 – Load
Reads `airline_delay.csv` into a pandas DataFrame and performs an initial inspection of shape, data types, and missing values.

### Step 2 – Clean & Transform
- Standardizes column names (lowercase, underscores)
- Fills missing values — median for numeric columns, mode for categorical
- Drops duplicate rows
- Casts `year` and `month` to integers; coerces delay/arrival columns to numeric

**Feature Engineering:**
- `total_delay` — sum of all delay components (carrier, weather, NAS, security, late aircraft)
- `on_time` — binary flag where arrival delay ≤ 0 minutes
- `delay_category` — bucketed severity label: *On Time / Minor / Moderate / Severe / Very Severe*

### Step 3 – Save
Exports the cleaned dataset to `airline_delay_cleaned.csv`.

### Step 4 – Visualize
Six charts are generated and saved as PNG files:

| File | Description |
|------|-------------|
| `viz_01_correlation_heatmap.png` | Lower-triangle correlation heatmap of all numeric features |
| `viz_02_distributions.png` | Histograms + KDE for 6 key delay columns |
| `viz_03_carrier_delay_bar.png` | Average arrival delay by carrier (top 15) |
| `viz_04_monthly_trend.png` | Average arrival delay by month |
| `viz_05_delay_categories.png` | Flight count per delay severity bucket |
| `viz_06_delay_components_boxplot.png` | Boxplot of each delay type (delayed flights only) |

### Step 5 – Key Findings
- The majority of flights are on time; delay distributions are heavily right-skewed — a small number of extreme delays pull averages up significantly.
- **Late aircraft** and **carrier delays** are the largest contributors; weather delays are less frequent but can be extreme.
- **Summer months (June–August)** show noticeably higher average delays, likely driven by thunderstorms and increased traffic volume.
- There is a meaningful spread in on-time performance **across airlines** — some carriers are consistently worse than others.
- Delay types are positively correlated with each other, reflecting the downstream cascade effect of a late arriving aircraft.
- **Security delays** are negligible compared to all other delay types.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
```

Install with:

```bash
pip install pandas numpy matplotlib seaborn
```

---

## Usage

1. Download `airline_delay.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data) and place it in the project root.
2. Launch Jupyter and open `airline_delay_pipeline.ipynb`.
3. Run all cells. The cleaned CSV and all visualization PNGs will be saved to the working directory.

---

## Project Structure

```
.
├── airline_delay_pipeline.ipynb   # Main notebook
├── airline_delay.csv              # Raw data (not tracked — download from Kaggle)
├── airline_delay_cleaned.csv      # Output: cleaned dataset
├── viz_01_correlation_heatmap.png
├── viz_02_distributions.png
├── viz_03_carrier_delay_bar.png
├── viz_04_monthly_trend.png
├── viz_05_delay_categories.png
└── viz_06_delay_components_boxplot.png
```

---

## License

This project is for educational and analytical purposes. Dataset credit goes to [sriharshaeedala on Kaggle](https://www.kaggle.com/datasets/sriharshaeedala/airline-delay/data).
