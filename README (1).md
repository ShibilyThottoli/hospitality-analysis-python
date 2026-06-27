# AtliQ Hotels — Hospitality Data Analysis

Exploratory data analysis on hotel bookings data for **AtliQ Grands**, a hotel chain operating across four Indian cities, to understand occupancy trends, revenue patterns, and customer booking behavior.

## 📌 Overview

AtliQ Grands wanted to understand why their revenue and occupancy numbers were inconsistent across properties and cities. This project analyzes raw booking-level and aggregated booking data to clean inconsistencies, engineer an occupancy metric, and surface actionable insights on **occupancy, revenue, and ratings** across cities, room categories, and time periods.

## 🗂️ Dataset

The data is structured as a fact-dimension model with 5 CSV files in `datasets/`:

| File | Description |
|---|---|
| `fact_bookings.csv` | Booking-level transactional data (134,590 rows) — guests, room category, platform, revenue, ratings |
| `fact_aggregated_bookings.csv` | Daily aggregated bookings per property — capacity vs. successful bookings |
| `dim_hotels.csv` | 25 hotel properties with city and category (Luxury / Business) |
| `dim_rooms.csv` | Room category mapping (RT1–RT4 → Standard, Elite, Premium, Presidential) |
| `dim_date.csv` | Calendar table with weekday/weekend flags and month labels |

## 🛠️ Tools & Libraries

- Python
- pandas
- Matplotlib (via pandas `.plot()`)

## 🔍 Approach

1. **Data Import & Exploration** — loaded all 5 datasets, explored shapes, unique values, and booking platform distribution
2. **Data Cleaning**
   - Removed bookings with invalid (≤0) guest counts
   - Removed revenue outliers using the **mean ± 3×standard deviation** rule
   - Identified and handled nulls — left `ratings_given` nulls untouched (58% missing, no safe imputation) and filled missing `capacity` values with the median
   - Filtered records where successful bookings exceeded property capacity (data errors)
3. **Data Transformation**
   - Engineered an **occupancy percentage** column (`successful_bookings / capacity`)
   - Merged fact tables with room, hotel, and date dimensions for richer grouping
   - Appended a new month's data (August) to validate the pipeline against incoming data
4. **Insights Generation** — grouped and aggregated across room category, city, weekday/weekend, and month

## 📊 Key Findings

- **Weekend occupancy (72.3%) is far higher than weekday occupancy (50.9%)** — a ~21-point gap, suggesting AtliQ's customer base is leisure/weekend-driven rather than business travel.
- **Delhi has the highest average occupancy (61.5%)**, ahead of Hyderabad (58.1%), Mumbai (57.9%), and Bangalore (56.3%).
- **Mumbai generates the highest revenue (₹66.9 Cr)** of all four cities despite not having the top occupancy — followed by Bangalore (₹42 Cr), Hyderabad (₹32.5 Cr), and Delhi (₹29.4 Cr).
- Occupancy is fairly even across room classes (~58–59%), with **Presidential rooms slightly ahead at 59.3%**, indicating premium rooms aren't sitting empty.
- **Atliq Exotica is the top-earning property** (₹32 Cr revenue), while **Atliq Seasons trails significantly** (₹6.6 Cr) — a clear outlier worth investigating.
- Average customer ratings are consistent across cities (3.4–3.8 out of 5), with **Delhi rating highest (3.78)** and **Bangalore lowest (3.41)**.
- Booking is dominated by **OTA aggregators** — "others" and MakeMyTrip together account for over 60% of all bookings, with direct bookings (online + offline) making up a relatively small share.

## 🚀 How to Run

```bash
git clone <repo-url>
cd <repo-folder>
pip install pandas matplotlib jupyter
jupyter notebook hospitality_analysis_project.ipynb
```

## 📁 Project Structure

```
├── datasets/
│   ├── dim_date.csv
│   ├── dim_hotels.csv
│   ├── dim_rooms.csv
│   ├── fact_aggregated_bookings.csv
│   ├── fact_bookings.csv
│   └── new_data_august.csv
├── hospitality_analysis_project.ipynb
└── README.md
```

## ✍️ Author

**Shibily Thottoli**
[LinkedIn](https://www.linkedin.com/in/shibily-thottoli) — Data Science Graduate | ML & NLP Enthusiast
