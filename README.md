# Predicting SpaceX Falcon 9 First-Stage Landing Success

An end-to-end data science project that predicts whether a SpaceX Falcon 9 first stage will land successfully. Because first-stage reuse is a key driver of launch economics, the prediction provides a practical signal for assessing launch cost and operational risk.

This project was completed as part of the IBM Data Science Professional Certificate capstone and is presented here as a reproducible portfolio case study.

## Why it matters

SpaceX advertises Falcon 9 launches at roughly **$62M**, while comparable launches can cost substantially more. Successful first-stage recovery enables reuse; estimating recovery likelihood before launch can therefore support cost and mission-planning decisions.

## Highlights

- Built a full analytics workflow from raw data acquisition to model evaluation.
- Combined SpaceX API data with web-scraped launch records and SQL-based exploration.
- Engineered launch features including launch site, orbit, payload mass, booster version, and landing outcome.
- Compared Logistic Regression, Support Vector Machine, Decision Tree, and K-Nearest Neighbors using 10-fold cross-validation.
- Selected a **Decision Tree** as the best validation model, reaching **90.36% cross-validation accuracy**. Each tuned model achieved **83.33% accuracy on the held-out test set**.
- Created an interactive Plotly Dash application for launch-site success and payload analysis.

## Project workflow

```text
SpaceX API + Wikipedia records
            |
      Data collection
            |
  Cleaning, SQL analysis, EDA
            |
 Feature engineering & encoding
            |
 Model tuning and evaluation
            |
 Landing-success prediction + dashboard
```

## Model results

| Model | Best cross-validation accuracy |
| --- | ---: |
| Decision Tree | **90.36%** |
| K-Nearest Neighbors | 84.82% |
| Support Vector Machine | 84.82% |
| Logistic Regression | 84.64% |

The final notebook uses `GridSearchCV` with 10-fold cross-validation. The selected tree used a Gini criterion, maximum depth of 6, `sqrt` feature sampling, and a minimum of 4 samples per leaf. Results should be interpreted in the context of the project dataset and split used in the notebook.

## Interactive dashboard

`spacex-dash-app.py` contains a Plotly Dash dashboard that lets users:

- Filter results by launch site.
- Compare successful launches across sites in a pie chart.
- Explore the relationship between payload mass and landing success.
- Color launch outcomes by booster-version category.

## Repository guide

| File | Purpose |
| --- | --- |
| `jupyter-labs-spacex-data-collection-api.ipynb` | Retrieves and prepares Falcon 9 launch records from the SpaceX API. |
| `jupyter-labs-webscraping.ipynb` | Extracts Falcon 9/Falcon Heavy launch data from Wikipedia with BeautifulSoup. |
| `labs-jupyter-spacex-Data wrangling.ipynb` | Cleans data and creates the landing-success target label. |
| `jupyter-labs-eda-sql-coursera_sqllite.ipynb` | Explores the dataset through SQL queries. |
| `edadataviz.ipynb` | Performs EDA, visualizations, and feature engineering. |
| `lab_jupyter_launch_site_location.ipynb` | Maps launch-site locations with Folium. |
| `SpaceX_Machine Learning Prediction_Part_5.ipynb` | Tunes, compares, and evaluates classification models. |
| `spacex-dash-app.py` | Runs the interactive launch-records dashboard. |

## Tools and techniques

**Python:** Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Plotly, Dash, BeautifulSoup, Folium

**Data work:** REST APIs, web scraping, SQL, data cleaning, feature encoding, exploratory analysis, interactive visualization

**Machine learning:** train/test split, standardization, classification, hyperparameter tuning, 10-fold cross-validation, confusion matrices

## Run the project

1. Clone the repository and create a virtual environment.

   ```bash
   git clone <repository-url>
   cd SpaceX-s-Falcon-9-rocket-Cost-Prediction
   python -m venv .venv
   ```

2. Activate the environment and install the libraries used by the notebooks and dashboard.

   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn plotly dash beautifulsoup4 requests folium jupyter
   ```

3. Open and run the notebooks in workflow order, starting with data collection.

   ```bash
   jupyter notebook
   ```

4. To launch the dashboard, ensure `spacex_launch_dash.csv` is available in the project root, then run:

   ```bash
   python spacex-dash-app.py
   ```

   Open the local URL printed by Dash in your browser.

## What I would improve next

- Package the data-preparation steps into a single reproducible pipeline.
- Add a versioned dataset and `requirements.txt` for one-command setup.
- Track precision, recall, ROC-AUC, and calibration alongside accuracy.
- Add automated tests and deploy the dashboard for a shareable demo.

---

If you are reviewing this project, start with the machine-learning notebook for the model-selection work, then open the Dash application to explore the launch patterns interactively.
