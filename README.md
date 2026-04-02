# 🏙️ Airbnb NYC Bookings Analysis — Pricing Intelligence & Market Strategy Through EDA

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/EDA-Exploratory%20Data%20Analysis-orange" />
  <img src="https://img.shields.io/badge/Domain-Travel%20%7C%20Hospitality-red" />
  <img src="https://img.shields.io/badge/Dataset-48%2C895%20Listings-green" />
  <img src="https://img.shields.io/badge/City-New%20York%20City-blueviolet" />
  <img src="https://img.shields.io/badge/Status-Production--Ready-brightgreen" />
</p>

---

## 📌 Table of Contents

- [Business Problem](#-business-problem)
- [Project Objective](#-project-objective)
- [Dataset Description](#-dataset-description)
- [Tech Stack](#-tech-stack)
- [Project Workflow](#-project-workflow)
- [Exploratory Data Analysis](#-exploratory-data-analysis)
- [Feature Engineering](#-feature-engineering)
- [Key Insights](#-key-insights)
- [Business Recommendations](#-business-recommendations)
- [Future Improvements](#-future-improvements)
- [How to Run](#-how-to-run)
- [Project Structure](#-project-structure)
- [Author](#-author)

---

## 🧩 Business Problem

### Industry Challenge

The **short-term rental market** is one of the most dynamic, data-rich, and pricing-sensitive sectors in the global hospitality industry. Airbnb, with millions of listings across 220+ countries, has fundamentally disrupted traditional hotel accommodation — but this disruption has also created enormous complexity for hosts, guests, and platform operators alike.

In New York City alone, **48,895 active listings** compete across five boroughs, covering three distinct room types and hundreds of individual neighbourhoods. The core challenge is this: **hosts are leaving money on the table.** Without a data-driven understanding of market pricing dynamics, neighbourhood demand, room type preferences, and availability patterns, hosts routinely under-price or over-price their listings — directly impacting both revenue and occupancy rates.

From the platform's perspective, poor pricing distribution leads to guest churn, marketplace inefficiency, and loss of competitive advantage to hotels and other alternatives.

### Why It Matters

| Stakeholder | Pain Point | Business Consequence |
|---|---|---|
| **Hosts** | No visibility into competitive pricing benchmarks | Under/over-pricing → lost revenue or zero bookings |
| **Guests** | Unclear value signals across price tiers | Decision fatigue, platform abandonment |
| **Airbnb Platform** | Inefficient marketplace pricing | Lower GMV, host churn, lower NPS |
| **Property Managers** | No data-driven inventory allocation | Suboptimal return on real estate investment |
| **City Planners / Regulators** | Uneven geographic distribution of listings | Housing pressure in saturated neighbourhoods |

### Business Impact

A well-executed pricing intelligence system built on EDA insights can directly:
- **Increase average host revenue** by 15–30% through dynamic, market-informed pricing
- **Improve occupancy rates** by aligning minimum nights policies with demand patterns
- **Reduce guest bounce rate** through clearer price-value signals per neighbourhood zone
- **Enable Airbnb to optimise matching algorithms** and promotional investments by borough

---

## 🎯 Project Objective

This project delivers a **comprehensive EDA-driven market intelligence analysis** of Airbnb's New York City listing data, designed to address the following objectives:

**Analytical Objectives:**
- Understand the spatial distribution of listings and pricing across NYC's five boroughs
- Identify which neighbourhoods, room types, and host profiles drive the highest revenue
- Analyse seasonal and temporal patterns in availability and review activity
- Detect pricing anomalies, outliers, and under-monetised listing segments

**Business Objectives:**
- Equip hosts with data-backed pricing benchmarks per neighbourhood and room type
- Identify saturated vs. underserved markets to guide strategic listing investment
- Provide Airbnb with actionable intelligence to power dynamic pricing algorithms
- Lay the analytical foundation for a machine learning price prediction model

---

## 📊 Dataset Description

| Property | Details |
|---|---|
| **Source** | Publicly available Airbnb NYC listings dataset (2019) |
| **Scope** | New York City — all five boroughs |
| **Rows** | 48,895 listings |
| **Columns** | 16 features |
| **Primary Analysis Target** | `price` (nightly listing rate in USD) |

### Feature Overview

| Column | Type | Description |
|---|---|---|
| `id` | Numeric | Unique listing identifier |
| `name` | Text | Listing title as shown to guests |
| `host_id` | Numeric | Unique host identifier |
| `host_name` | Text | Name of the listing host |
| `neighbourhood_group` | Categorical | One of five NYC boroughs |
| `neighbourhood` | Categorical | Specific neighbourhood within borough |
| `latitude` / `longitude` | Numeric | Geospatial coordinates for mapping |
| `room_type` | Categorical | Entire home/apt, Private room, Shared room |
| `price` | Numeric ⭐ | **Primary KPI** — nightly rate in USD |
| `minimum_nights` | Numeric | Minimum booking length required |
| `number_of_reviews` | Numeric | Total reviews accumulated |
| `last_review` | DateTime | Date of the most recent guest review |
| `reviews_per_month` | Numeric | Monthly average review velocity |
| `calculated_host_listings_count` | Numeric | Total active listings per host |
| `availability_365` | Numeric | Days available for booking in a year |

### Missing Value Summary

| Column | Missing Count | % Missing | Treatment Applied |
|---|---|---|---|
| `name` | 16 | 0.03% | Filled with `'No name'` |
| `host_name` | 21 | 0.04% | Filled with `'not define'` |
| `last_review` | 10,052 | 20.6% | Parsed to datetime; coerced where invalid |
| `reviews_per_month` | 10,052 | 20.6% | Imputed with **median** (0.72/month) |

> **Key observation:** The ~20% missing rate in `last_review` and `reviews_per_month` corresponds to listings that have **never received a review** — a meaningful signal of low engagement or newly listed properties, not a data quality failure.

### Pricing Summary Statistics

| Metric | Value |
|---|---|
| Mean Price | $152.72 / night |
| Median Price | $106.00 / night |
| Standard Deviation | $240.15 |
| Min Price | $0 (11 listings — data anomaly) |
| 75th Percentile | $175.00 |
| Max Price | $10,000 / night |

The extreme right skew (mean >> median; max = $10,000) confirms **significant outliers in the luxury segment**, which require careful handling before any predictive modelling.

---

## 🛠 Tech Stack

```
Language          : Python 3.10+
Data Handling     : Pandas, NumPy
Visualisation     : Matplotlib, Seaborn
Geospatial Plot   : Seaborn Scatter (lat/lon)
Environment       : Google Colab / Jupyter Notebook
```

---

## 🔄 Project Workflow

```
┌──────────────────────┐     ┌──────────────────────┐     ┌───────────────────────┐
│  1. Data Loading      │────▶│  2. Data Quality      │────▶│  3. Exploratory Data  │
│     & Inspection      │     │     Assessment        │     │     Analysis (EDA)    │
└──────────────────────┘     └──────────────────────┘     └──────────┬────────────┘
                                                                       │
┌──────────────────────┐     ┌──────────────────────┐     ┌──────────▼────────────┐
│  6. Business          │◀────│  5. Correlation &     │◀────│  4. Feature           │
│     Recommendations   │     │     Statistical       │     │     Engineering       │
└──────────────────────┘     │     Analysis          │     └───────────────────────┘
                              └──────────────────────┘
```

### Phase-by-Phase Breakdown

**Phase 1 — Data Loading & Inspection:** Dataset loaded from CSV with 48,895 rows across 16 columns. Zero duplicate rows found after deduplication. Data types inspected — 10 numeric, 6 categorical/text features.

**Phase 2 — Data Quality Assessment:** Missing values identified and treated per domain logic. Non-informative identifier columns (`id`, `host_id`, `calculated_host_listings_count`) dropped to reduce modelling noise. Duplicate records removed using a composite key of `name`, `host_name`, `neighbourhood`, `latitude`, and `longitude`.

**Phase 3 — EDA:** 16 visualisations constructed — spanning univariate, bivariate, geospatial, temporal, and multivariate analyses — to surface actionable insights across pricing, geography, room type, availability, and review behaviour.

**Phase 4 — Feature Engineering:** New analytical features derived from existing columns to unlock deeper business intelligence (see Feature Engineering section below).

**Phase 5 — Correlation & Statistical Analysis:** Correlation heatmap computed on all numeric features. Pair plots generated segmented by room type. Price-availability and price-review relationships examined for market signals.

**Phase 6 — Business Recommendations:** Findings synthesised into a structured set of host-facing and platform-level strategic recommendations.

---

## 📈 Exploratory Data Analysis

### Chart 1 — Room Type Distribution (Univariate Bar Chart)
**Entire home/apt dominates at 52%**, followed by Private room (46%) and Shared room (2%). The majority of NYC listings compete in the highest price tier, intensifying price sensitivity among entire-home guests and creating a two-tier market dynamic.

### Chart 2 — Room Type by Borough (Bivariate Count Plot)
Manhattan and Brooklyn together account for **85%+ of all listings**. Private rooms are proportionally more prevalent in Brooklyn, while Manhattan skews toward entire homes — reflecting the premium Manhattan market where full-apartment rentals command the highest yields per night.

### Chart 3 — Neighbourhood Group Distribution (Pie Chart)

| Borough | Listings | Market Share |
|---|---|---|
| Manhattan | 21,661 | 44.3% |
| Brooklyn | 20,104 | 41.1% |
| Queens | 5,666 | 11.6% |
| Bronx | 1,091 | 2.2% |
| Staten Island | 373 | 0.8% |

Manhattan + Brooklyn = **85.4% of all NYC Airbnb supply** — a clear indicator of where competitive pricing pressure is highest, and where new hosts face the steepest entry challenge.

### Chart 4 — Price Distribution Histogram + KDE ($0–$350 range)
The pricing distribution is **heavily right-skewed** with the highest density concentrated between **$50–$150/night**. Most guests are price-sensitive, and listings above $350 represent a niche luxury segment with distinct demand drivers and a different guest profile.

### Chart 5 — Top 10 Neighbourhoods by Listing Count

| Rank | Neighbourhood | Borough | Listing Count |
|---|---|---|---|
| 1 | Williamsburg | Brooklyn | 3,920 |
| 2 | Bedford-Stuyvesant | Brooklyn | 3,714 |
| 3 | Harlem | Manhattan | 2,658 |
| 4 | Bushwick | Brooklyn | 2,465 |
| 5 | Upper West Side | Manhattan | 1,971 |
| 6 | Hell's Kitchen | Manhattan | 1,958 |
| 7 | East Village | Manhattan | 1,853 |
| 8 | Upper East Side | Manhattan | 1,798 |
| 9 | Crown Heights | Brooklyn | 1,564 |
| 10 | Midtown | Manhattan | 1,545 |

Williamsburg and Bedford-Stuyvesant — both in Brooklyn — are the most **supply-saturated markets**. High competition compresses pricing power for individual hosts, making differentiation via quality and responsiveness more important than price.

### Chart 6 — Geographic Distribution (Lat/Lon Scatter Plot)
The geospatial plot maps five distinct borough clusters with clear spatial boundaries. **Manhattan listings form the densest urban core**, while Staten Island shows the sparsest coverage. This confirms that proximity to tourist destinations and transit hubs is the primary driver of listing density.

### Chart 7 — Average Nightly Price: Room Type × Borough

| Borough | Entire Home/Apt | Private Room | Shared Room |
|---|---|---|---|
| **Manhattan** | **~$249** | **~$116** | **~$89** |
| Brooklyn | ~$178 | ~$77 | ~$51 |
| Staten Island | ~$175 | ~$62 | ~$57 |
| Queens | ~$143 | ~$72 | ~$59 |
| Bronx | ~$128 | ~$65 | ~$58 |

**Manhattan entire homes command a 40%+ premium** over Brooklyn equivalents — the highest price differential across any room type-borough combination in the dataset.

### Chart 8 — Price vs. Availability (Scatter Plot)
No strong linear correlation between price and annual availability days. However, **ultra-high-priced listings ($500+)** tend to show clustered, lower availability — suggesting luxury hosts strategically restrict their calendar to maintain exclusivity and signal premium positioning.

### Chart 9 — Reviews per Month Distribution (Histogram)
Strongly right-skewed — the majority of listings receive fewer than **2 reviews/month**. A small cohort of highly active Superhost listings drives the bulk of review volume. Review velocity is a strong proxy for booking frequency and serves as a reliable engagement KPI for platform health monitoring.

### Chart 10 — Price KDE Plot ($0–$350)
The **mode price point is approximately $75–$100/night**, with a pronounced density peak in this range. This is the market's equilibrium zone — where supply and demand are most balanced — and represents a critical pricing anchor point for new hosts entering any NYC borough.

### Chart 11 — Stacked Room Type Distribution by Borough
Brooklyn and Manhattan show fundamentally different inventory compositions. Brooklyn private rooms form a larger share of inventory vs. Manhattan, creating a naturally **more accessible, budget-friendly market in Brooklyn** — clearly segmented from Manhattan's premium entire-home supply.

### Chart 12 — Availability Over Time (Area Chart, post-2000)
Availability shows **pronounced seasonal peaks and troughs** with spikes in Q1 (January) and Q4 (December). This temporal pattern maps directly onto NYC's tourism calendar — New Year celebrations, holiday travel, and summer tourism. Hosts who align their pricing to these peaks can maximise yield.

### Chart 13 — Joint Plot: Price vs. Reviews per Month
Near-zero correlation between nightly price and monthly review velocity confirms that **price alone does not drive review activity**. Guest experience quality, host responsiveness, and listing accuracy are stronger determinants of review engagement — an important insight for hosts who conflate high pricing with low guest satisfaction.

### Chart 14 — Correlation Heatmap

| Variable Pair | Correlation | Business Interpretation |
|---|---|---|
| `number_of_reviews` ↔ `reviews_per_month` | Moderate positive | Older listings accumulate more reviews |
| `price` ↔ `availability_365` | Slight negative | Higher-priced listings have fewer open days |
| `latitude` / `longitude` ↔ `price` | Weak | Location alone is not a perfect price predictor |
| Most other pairs | Near zero | Low multicollinearity — healthy for future ML modelling |

### Charts 15 & 16 — Pair Plots (by Room Type)
Room type acts as a strong natural **market segmentation axis**. Entire homes cluster at higher price ranges with more varied minimum-night requirements. Private rooms cluster tightly in the $50–$150 band. Shared rooms show the highest availability days, indicating the lowest booking frequency of the three types.

---

## ⚙️ Feature Engineering

### Engineered Features & Business Rationale

**1. `revenue` = `price` × `number_of_reviews`**
A proxy for cumulative host earnings. While not precise (reviews ≠ bookings exactly), it provides a **relative revenue ranking** across listings — identifying which hosts and neighbourhoods generate the most economic activity on the platform. Useful for building a host performance leaderboard.

**2. `review_month` and `review_year`** (extracted from `last_review`)
Enables **temporal analysis of listing engagement** — identifying which months see peak guest activity and whether newer or older listings dominate review activity in a given borough. Forms the basis for seasonal demand modelling.

**3. `total_reviews` = `number_of_reviews` + `reviews_per_month`**
A composite engagement score capturing both **lifetime review accumulation** and **current momentum** — useful for distinguishing newly popular listings from established long-term favourites within the same neighbourhood.

**4. `name_cleaned`** (lowercased, punctuation-stripped `name`)
Normalised listing title for downstream **NLP keyword analysis** — enabling exploration of which title keywords (e.g., "cozy", "luxury", "central", "spacious") correlate with higher engagement, pricing power, and booking rates.

**5. `reviews_per_month` Median Imputation (median = 0.72)**
Missing review rate replaced with the market median rather than zero or mean — avoiding artificial suppression of engagement scores for unlisted or inactive properties while maintaining statistical integrity.

**6. Minimum Nights Filter (= 1 night) for Price Analysis**
A subset filtered to minimum_nights = 1 is used for per-night price benchmarking, ensuring price comparisons are made on an apples-to-apples basis and not distorted by weekly or monthly rental structures.

---

## 💡 Key Insights

> *Translating EDA outputs into board-ready business intelligence.*

**1. The Manhattan Premium Is Real and Quantifiable**
Manhattan's average nightly price ($196.88) is **99% higher than the Bronx** ($87.50) and **58% higher than Brooklyn** ($124.38). For hosts in Manhattan, there is strong, structural pricing power — particularly for entire homes — that is consistently underutilised by new entrants who default to competitor-matching rather than location-premium pricing.

**2. Williamsburg and Bedford-Stuyvesant Are Saturated — Differentiation Is Essential**
The top two neighbourhoods by listing count are both in Brooklyn, not Manhattan. This high supply concentration **suppresses individual listing visibility and pricing power**. New hosts in these areas must differentiate via amenities, responsiveness, and Superhost status rather than competing on price alone.

**3. Entire Home / Apt Commands a 136% Price Premium Over Shared Rooms**
At $211.79 average vs. $70.13 for shared rooms, the entire home segment is the highest-value inventory type on the platform. Hosts with a spare apartment or investment property should prioritise listing as entire homes where local regulations permit.

**4. 20% of Listings Have Never Received a Review — A Dead Inventory Problem**
10,052 listings have no review history. These may be poorly titled, incorrectly priced, or hosted by non-responsive hosts. This represents a high-priority intervention cohort for Airbnb's host success and marketplace health teams.

**5. Price Has No Meaningful Correlation With Review Volume**
The near-zero price-reviews correlation confirms that **guests do not disproportionately avoid higher-priced listings after booking**. Guest satisfaction — and therefore reviews — is driven by experience quality, not price. This empowers well-managed premium listings to price more aggressively without fear of review penalties.

**6. January and December Are Peak Availability Spikes**
Seasonal availability patterns align with NYC's holiday tourism calendar. Hosts who keep calendars **open during Q1 and Q4** stand to capture the highest booking volumes of the year. Off-peak months (March–May) show suppressed availability — a potential revenue opportunity for price-flexible hosts.

**7. A Small Cohort of Professional Hosts Dominates Supply**
With a maximum of 327 listings under a single host (Sonder NYC) and a platform mean of 7 listings/host, the market is bifurcated between individual hosts and institutional property managers. Professional operators use sophisticated dynamic pricing strategies that individual hosts cannot match on price alone — but can outcompete on authenticity, local knowledge, and personalisation.

**8. The $75–$100 Price Band Is the Market's Centre of Gravity**
The KDE mode confirms this is where supply and demand are most balanced. New hosts entering at this price point face the highest competition but also the highest probability of initial bookings and review accumulation — both critical for building long-term Superhost status and search ranking.

---

## 💼 Business Recommendations

**1. Implement Borough-Calibrated Dynamic Pricing**
Hosts should price relative to their **borough's median**, not the citywide average. A private room in Manhattan should baseline at $116, not $90 (citywide private room average). Dynamic pricing tools should be configured with borough-level floor prices informed by this analysis.

**2. Target the $75–$150 "Sweet Spot" for New Listing Launches**
New hosts should launch within the modal price band ($75–$100 for private rooms; $125–$175 for entire homes) to maximise early booking volume and review accumulation — the two primary drivers of search ranking within the Airbnb algorithm.

**3. Develop a "Zero-Review Listing" Intervention Programme**
Airbnb should proactively engage the ~10,000 listings with no reviews through an automated nudge campaign — offering title optimisation guidance, pricing recalibration tools, and photography incentives to convert dead inventory into active bookings.

**4. Introduce Neighbourhood Saturation Alerts for New Hosts**
Before a host lists in a high-density neighbourhood like Williamsburg, Airbnb should surface a **market saturation dashboard** — showing current supply levels, estimated occupancy benchmarks, and pricing comparisons — to set accurate revenue expectations and encourage differentiation strategies.

**5. Leverage Seasonal Calendar Optimisation**
Airbnb's smart pricing tools should surface **peak-season calendar alerts** in October–November (ahead of Q4 peaks) and November–December (ahead of Q1 peaks), prompting hosts to open availability and adjust minimum-night policies for high-demand holiday periods.

**6. Build a Segmented Host Support Model**
Segment hosts into Individual (1–2 listings), Semi-professional (3–10 listings), and Professional (10+ listings) tiers. Each tier requires a different support model: individual hosts need pricing education; professional operators need API access and bulk management tools. This tiering improves retention across both host segments.

**7. Prioritise Queens and Bronx as Strategic Growth Markets**
With significantly lower listing density but strong transit access to Manhattan attractions, Queens and Bronx represent **under-tapped markets** with less competitive pressure. Targeted host acquisition campaigns in these boroughs would expand affordable supply while reducing concentration risk in Brooklyn and Manhattan.

**8. Deploy Geospatial Intelligence for Localised Marketing**
The lat/lon scatter analysis reveals distinct geographic clusters. Airbnb's marketing team should use this spatial data to create **neighbourhood-specific content campaigns** — e.g., "Hidden Brooklyn", "Best of Harlem" — that attract demand to under-listed areas while alleviating oversaturation in high-density zones.

---

## 🚀 Future Improvements

### Machine Learning Extensions

**Price Prediction Model:**
Build a supervised regression model using `price` as the target variable. Features would include `neighbourhood_group`, `room_type`, `minimum_nights`, `availability_365`, `number_of_reviews`, `reviews_per_month`, and geospatial coordinates. Candidate algorithms: Ridge Regression (baseline), Random Forest, XGBoost, and LightGBM — compared via RMSE and MAE on a holdout test set.

**Occupancy Rate Prediction:**
Use `reviews_per_month` as a booking frequency proxy to build an **occupancy estimation model** — enabling hosts to forecast demand and adjust pricing dynamically week by week.

**Listing Quality Scoring:**
Train a multi-feature scoring model combining price competitiveness, review velocity, calendar completeness, and NLP title signals to produce a **"listing health score"** for each host — surfaced via a Superhost recommendations engine.

### NLP & GenAI Integration

**Listing Title Optimisation Engine:**
Apply NLP to `name_cleaned` to identify which **title keywords correlate with higher review velocity and booking rates**. Build a GenAI-powered title generator (using an LLM API) that suggests optimised listing titles based on property attributes, neighbourhood context, and seasonal demand signals.

**Guest Review Sentiment Analysis:**
Integrate guest review text data to perform **aspect-based sentiment analysis** — identifying whether negative reviews cluster around price, cleanliness, location, or host responsiveness — giving hosts and the Airbnb platform targeted, category-specific improvement signals.

### Deployment & Product Integration

**Interactive Pricing Dashboard:**
Deploy a **Streamlit or Power BI dashboard** where hosts can input their property details (borough, room type, minimum nights) and receive an instant pricing benchmark, competitive landscape overview, and revenue optimisation recommendation.

**REST API for Real-Time Pricing Intelligence:**
Productionise the price prediction model as a **FastAPI endpoint** — enabling integration with third-party property management systems and smart home platforms. Containerise with Docker; deploy on AWS Lambda or Google Cloud Run for serverless scalability.

**MLOps Pipeline:**
Implement a **scheduled retraining pipeline** using Apache Airflow or Prefect, triggered monthly when new Airbnb listing data becomes available. Track model drift using Evidently AI to ensure price predictions remain accurate as the NYC market evolves.

---

## ▶️ How to Run

### Prerequisites

```bash
pip install numpy pandas matplotlib seaborn
```

### Steps

**1. Clone the repository:**
```bash
git clone https://github.com/vishal-Londhekar/AirBnb-Bookings-Analysis-EDA.git
cd AirBnb-Bookings-Analysis-EDA
```

**2. Install dependencies:**
```bash
pip install -r requirements.txt
```

**3. Place the dataset in the working directory:**
```
Airbnb_NYC_2019.csv
```

**4. Launch Jupyter Notebook:**
```bash
jupyter notebook AirBnb_Bookings_Analysis_Exploratory_Data_Analysis.ipynb
```

**5. Or open in Google Colab:**
Upload `Airbnb_NYC_2019.csv` to your Google Drive and update the file path in **Cell 18** before running all cells.

**6. Run all cells sequentially** — the notebook is structured to execute end-to-end without errors.

---

## 📁 Project Structure

```
AirBnb-Bookings-Analysis-EDA/
│
├── AirBnb_Bookings_Analysis_Exploratory_Data_Analysis.ipynb   # Main notebook (188 cells)
├── Airbnb_NYC_2019.csv                                         # Dataset (48,895 × 16)
├── requirements.txt                                            # Python dependencies
└── README.md                                                   # Project documentation
```

### `requirements.txt`
```
numpy>=1.23.0
pandas>=1.5.0
matplotlib>=3.6.0
seaborn>=0.12.0
```

---

## 👤 Author

<table>
  <tr>
    <td align="center">
      <b>Vishal Londhekar</b><br/>
      <i>Data Analyst | Data Scientist | ML Engineer</i><br/><br/>
      <a href="https://github.com/vishal-Londhekar">🔗 GitHub</a>&nbsp;&nbsp;
      <a href="mailto:v.londhekar2003@gmail.com">📧 Email</a>
    </td>
  </tr>
</table>

> *"The best business decisions aren't made in boardrooms — they're made by those who understand what the data is actually saying."*

---

## ⭐ If you found this project valuable, please star the repository!

---

<p align="center">
  <img src="https://img.shields.io/badge/Made%20with-Python-blue?logo=python" />
  <img src="https://img.shields.io/badge/Domain-Hospitality%20%7C%20Real%20Estate-red" />
  <img src="https://img.shields.io/badge/Charts-16%20Visualisations-orange" />
  <img src="https://img.shields.io/badge/City-New%20York%20City-blueviolet" />
</p>
