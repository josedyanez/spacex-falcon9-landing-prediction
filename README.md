# 🚀 SpaceX Falcon 9 — First-Stage Landing Prediction

End-to-end data science project: collecting launch data from an API and web scraping, cleaning it, exploring it with SQL and visualizations, building an interactive map and dashboard, and training classification models to predict whether a Falcon 9 first stage will land successfully.

> Capstone project of the **IBM Data Science Professional Certificate** (Coursera, 2024).

---

## 🎯 Business question

Reusing the first stage is the main reason SpaceX launches are cheaper than its competitors'. If we can **predict whether the first stage will land**, we can estimate the cost of a launch. The project frames this from the point of view of a hypothetical new competitor ("Space Y") that wants to bid against SpaceX.

**Specific questions:**
1. Can we predict a successful first-stage landing from launch characteristics (payload, orbit, launch site, booster version)?
2. Which launch sites and conditions are associated with the highest success rates?

---

## 📌 Key results

| | |
|---|---|
| **Best model** | Decision Tree Classifier |
| **Test accuracy** | 94.4% (17 of 18 launches classified correctly) |
| **Validation accuracy (during tuning)** | > 87% |
| **Trend** | Landing success rose from 0% (2010–2013) to over 80% by 2017–2020 |
| **Site with most successful launches** | KSC LC-39A (41.7% of all successes; 76.9% success rate at that site) |

**Main insights from the analysis:**
- Landing success improves steadily over time, reflecting the evolution of the rocket and the process.
- Orbits ES-L1, GEO, HEO and SSO show the highest success rates; GTO shows no clear relationship between payload and success.
- Payloads above ~9,000 kg show a high success rate, and payloads above 12,000 kg were only launched from CCAFS SLC-40 and KSC LC-39A.
- Launch sites are located close to the coast (for safety) while staying near roads and railroads (for logistics), and most launches happen on the U.S. east coast.

---

## 🛠️ Pipeline

| Step | What was done | Notebook / file |
|---|---|---|
| 1. Data collection (API) | Requested launch data from the SpaceX REST API, filtered Falcon 9 launches and handled missing values | [Data collection – API](jupyter-labs-spacex-data-collection-api.ipynb) |
| 2. Data collection (scraping) | Scraped the Falcon 9 launch tables from Wikipedia with BeautifulSoup into a DataFrame | [Web scraping](jupyter-labs-webscraping.ipynb) |
| 3. Data wrangling | Explored launches per site and orbit, and created the binary landing-outcome label | [Data wrangling](labs-jupyter-spacex-Data%20wrangling.ipynb) |
| 4. EDA with SQL | 10 SQL queries on SQLite (aggregations, filters, date ranges, ranking of landing outcomes) | [EDA with SQL](jupyter-labs-eda-sql-coursera_sqllite.ipynb) |
| 5. EDA with visualization | Scatter, bar and line plots of payload, orbit, site and flight number vs. outcome | [EDA with visualization](jupyter-labs-eda-dataviz.ipynb.jupyterlite.ipynb) |
| 6. Interactive map | Folium map with launch sites, success/failure markers and distances to coast, roads and railroads | [Launch site map](lab_jupyter_launch_site_location.jupyterlite%20%281%29.ipynb) |
| 7. Dashboard | Plotly Dash app: success share by site, success ratio per site, and payload vs. outcome by booster version | [Dash app](dash_spaceX.py) |
| 8. Machine learning | Standardization, train/test split and hyperparameter search over Logistic Regression, SVM, Decision Tree and KNN | [ML prediction](SpaceX_Machine_Learning_Prediction_Part_5.jupyterlite.ipynb) |

The full write-up with all charts is in the [project report (PDF)](CapstoneReport-JoseYanez.pdf).

---

## 🤖 Model comparison

| Model | Test accuracy |
|---|---|
| Logistic Regression | 83.3% |
| Support Vector Machine | 83.3% |
| **Decision Tree** | **94.4%** |
| K-Nearest Neighbors | 83.3% |

For each model, several hyperparameter combinations were evaluated on the training data, and the best one was then scored on the held-out test set.

### ⚠️ Limitations

- The test set has only **18 launches**, so one launch changes accuracy by about 5.6 points. The gap between the Decision Tree and the other models is **2 launches**, which is not enough to claim it is truly better.
- A more reliable comparison would use repeated cross-validation on the full dataset and report precision, recall and F1, not only accuracy.
- The dataset covers launches up to 2020; newer launches would likely change the picture.

---

## 🧰 Tech stack

**Python** · pandas · NumPy · requests · BeautifulSoup · **SQL (SQLite)** · Matplotlib · Seaborn · Folium · Plotly Dash · scikit-learn · Jupyter

---

## ▶️ How to run

```bash
git clone https://github.com/josedyanez/spacex-falcon9-landing-prediction.git
cd spacex-falcon9-landing-prediction
pip install pandas numpy requests beautifulsoup4 matplotlib seaborn folium dash scikit-learn jupyter
```

- Open the notebooks with Jupyter in the order shown in the pipeline table above.
- Run the dashboard with `python dash_spaceX.py` and open the local address it prints.

---

## 👤 Author

**Jose David Yanez** — Electronic Engineer · MS Computer Science student at CU Boulder
[LinkedIn](https://www.linkedin.com/in/josedyanez/) · [GitHub](https://github.com/josedyanez)
