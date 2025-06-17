# 📦 Delhivery Logistics Trip Analysis

A data wrangling and statistical exploration project on trip-level logistics data from **Delhivery**, one of India's leading supply chain services companies. The goal: understand the real-world delivery performance versus model-estimated routes (OSRM) and uncover operational inefficiencies.

---

## 🧰 Project Summary

- **Dataset**: ~145,000 rows of trip segment data from Delhivery.
- **Source**: CSV extracted via Google Colab from `delhivery_data.txt`
- **Focus**:
  - Cleaning and standardizing timestamps, distances, times.
  - Aggregating segment data to full trips.
  - Comparing actual vs. estimated time/distance.
  - Statistical testing (Shapiro, Mann-Whitney U) to validate differences.

---

## 📁 Structure

| Stage               | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `data load & prep` | Clean nulls, drop irrelevant fields, parse dates and convert types.         |
| `EDA`              | Distributions, missing values, datatypes, basic stats.                      |
| `feature engineering` | Break down location fields, extract datetime features (month, week, etc). |
| `aggregation`      | Summarize segments into trips via two-level grouping.                       |
| `hypothesis testing` | Statistically compare actual vs. estimated logistics performance.          |

---

## 🔍 Key Findings

### 🕓 1. `od_total_time` vs `start_scan_to_end_scan`
> These two time fields differ **significantly** (p-value = 0.000).  
> Interpretation: System-planned time ≠ actual scan-time execution.

### ⏱️ 2. `actual_time` vs `osrm_time`
> OSRM route times **underestimate** real delivery times (p-value = 0.000).  
> Implies model needs adjustment to reflect traffic, delays, handoffs.

### 🧱 3. `actual_time` vs `segment_actual_time`
> Aggregated segment times **do not capture** the full trip time.  
> Hidden delays (e.g., idle time, depot waits) may exist.

### 📏 4. `osrm_distance` vs `segment_osrm_distance`
> Segment-level distances **don’t add up** to the total OSRM route.  
> Possible route recalculations or data inconsistencies.

---

## 📊 Tools & Libraries

- 🐍 Python (Colab environment)
- 📦 `pandas`, `numpy` for data wrangling
- 📈 `matplotlib`, `seaborn` for visualization
- 🔬 `scipy.stats` for hypothesis testing

---

## 🧠 Takeaways

- **ETAs from OSRM are optimistic**; real trips take longer.
- **Segment-level data omits delay windows** — need better logging or buffer modeling.
- **Data-driven logistics optimization** must correct for real-world lag, not just shortest path.

---

## 📎 Notes

- All statistical tests accounted for non-normality (Shapiro-Wilk).
- Mann-Whitney U used for robust comparisons.
- Project extensible to include ML modeling (e.g., ETA prediction, delay classification).

---

## ✅ Next Steps

- Train a predictive model to correct OSRM ETA biases.
- Cluster trips by performance patterns.
- Build operational dashboards to monitor segment-level delays.

---

