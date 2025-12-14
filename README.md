# AirBnb Bookings Analysis — Exploratory Data Analysis (EDA)

Short exploratory data analysis of Airbnb bookings focused on pricing, seasonality, and listing characteristics.

**Repository summary**
- **Purpose:** Explore and visualize Airbnb booking data to surface insights for hosts and analysts.
- **Author:** Vishal Londhekar — v.londhekar2003@gmail.com

## Dataset
- `Airbnb NYC 2019.csv` — primary dataset used for the analysis (NYC listings and booking-related features).

## Contents
- `AirBnb_Bookings_Analysis_Exploratory_Data_Analysis (1).ipynb` — main Jupyter Notebook with cleaning, EDA, and visualizations.
- `Airbnb NYC 2019.csv` — dataset used by the notebook.
- `README.md` — this file.

## Dependencies
Recommended Python environment (Python 3.8+). Key packages:

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- jupyter

Install with pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

Or create a `requirements.txt` with the above packages and run:

```bash
pip install -r requirements.txt
```

## Quickstart — Open the Notebook
1. Open a terminal in the repository directory.
2. Start Jupyter Lab or Notebook:

```bash
jupyter notebook
```

3. Open the notebook `AirBnb_Bookings_Analysis_Exploratory_Data_Analysis (1).ipynb` and run cells sequentially.

## What the Notebook Does
- Loads `Airbnb NYC 2019.csv` and performs basic data cleaning (missing values, types, duplicates).
- Performs exploratory analysis: distributions, correlations, neighborhood price comparisons, and seasonal trends.
- Produces visualizations (histograms, boxplots, heatmaps, time trends) with commentary.

## Notes & Tips
- If the dataset is large, consider running heavy visualizations on a sampled subset.
- Use the notebook's section headings to jump to specific analyses (Data Cleaning → EDA → Visualizations).

## Contact
If you have questions or suggestions, reach out to the author at v.londhekar2003@gmail.com.

---

Enjoy exploring the data! 🚀
