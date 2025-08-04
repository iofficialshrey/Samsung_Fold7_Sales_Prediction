# Samsung Fold7 Sales Prediction

Predicting first-month sales of the Samsung Galaxy Z Fold 7 using historical Fold series data, Reddit sentiment, and feature-level buzz.

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)  
2. [Repository Structure](#repository-structure)  
3. [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Installation](#installation)  
4. [Data Pipeline](#data-pipeline)  
   1. [Data Collection](#data-collection)  
   2. [Data Cleaning & Preprocessing](#data-cleaning--preprocessing)  
   3. [Exploratory Data Analysis](#exploratory-data-analysis)  
   4. [Feature Engineering](#feature-engineering)  
   5. [Modeling & Evaluation](#modeling--evaluation)  
5. [Results](#results)  
6. [Usage](#usage)  
   - [Run Notebooks](#run-notebooks)  
   - [Run Streamlit App (Optional)](#run-streamlit-app-optional)  
7. [Project Insights](#project-insights)  
8. [Future Work](#future-work)  
9. [License](#license)

---

## Project Overview

Smartphone launches hinge on early market reception. We analyze the Samsung Galaxy Z Fold series (Fold 4–7) to:

- **Quantify social buzz and sentiment** via Reddit.  
- **Engineer feature-level metrics** (battery, camera, price, etc.).  
- **Train regression models** (Linear, RF, XGBoost) to predict sales.  
- **Forecast Fold 7’s first-month sales** and deliver actionable insights.

---

## Repository Structure

Samsung_Fold7_Sales_Prediction/
├── data/
│ ├── raw/ # Raw scraped CSVs + sales data
│ └── processed/ # Cleaned, sentiment, model-ready CSVs
├── models/ # Saved trained models (.pkl)
├── notebooks/
│ ├── 01_data_collection.ipynb
│ ├── 02_data_cleaning.ipynb
│ ├── 03_eda.ipynb
│ ├── 04_feature_engineering.ipynb
│ ├── 05_modeling.ipynb
│ └── 06_evaluation_and_optimization.ipynb
├── src/ # (Optional) helper modules with doc-strings
├── .gitignore
├── README.md
├── requirements.txt
└── environment.yml # (Optional) Conda environment file

less
Copy
Edit

---

## Getting Started

### Prerequisites

- Python 3.8–3.10  
- Git  
- (Recommended) [Conda](https://docs.conda.io/) or virtualenv  

### Installation

1. **Clone the repo**  
   ```bash
   git clone git@github.com:YOUR_USERNAME/Samsung_Fold7_Sales_Prediction.git
   cd Samsung_Fold7_Sales_Prediction
Create environment & install
With Conda:

bash
Copy
Edit
conda env create -f environment.yml
conda activate fold_sales_env
Or with pip:

bash
Copy
Edit
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
Data Pipeline
1. Data Collection
Notebooks: 01_data_collection.ipynb

Tools: PRAW (Reddit API), manual sales data lookup

Output: data/raw/foldX_reddit.csv, data/raw/fold6_fold7_sales.csv

2. Data Cleaning & Preprocessing
Notebook: 02_data_cleaning.ipynb

Steps: merge, lowercase, remove URLs/punctuation, parse timestamps

Output: data/processed/reddit_clean.csv

3. Exploratory Data Analysis
Notebook: 03_eda.ipynb

Analysis: post volumes, sentiment breakdown, feature‐mention trends

Output: data/processed/reddit_sentiment.csv

4. Feature Engineering
Notebook: 04_feature_engineering.ipynb

Engineering: binary feature flags, per‐feature mention counts & avg polarity

Output: data/processed/model_data.csv

5. Modeling & Evaluation
Notebook: 05_modeling.ipynb & 06_evaluation_and_optimization.ipynb

Models: Linear Regression, Random Forest, XGBoost, stacking example

Metrics: MAE, RMSE, R², residuals, learning curves

Output: models/fold_sales_model.pkl, data/processed/fold7_prediction.csv

Results
Best model: Random Forest (tuned) with MAE ≈ X units, R² ≈ Y%.

Predicted Fold 7 Sales: ~Z units in first month.

Key drivers: battery and camera sentiment most strongly correlated with uplift.

Usage
Run Notebooks
Launch Jupyter in the project root:

bash
Copy
Edit
jupyter notebook
Open and run the notebooks in sequence (01 → 06).

Run Streamlit App (Optional)
bash
Copy
Edit
streamlit run src/app.py
Then open http://localhost:8501 to interact with the dashboard.

Project Insights
Correlated positive sentiment on battery/camera with higher sales.

Identified features (price, hinge) where sentiment lags and potential R&D focus.

Demonstrated how social data can inform early sales forecasts.

Future Work
Incorporate Google Trends or YouTube review data.

Expand to other Fold series or competitor foldables.

Deploy the trained model as a REST API (FastAPI/Flask).

Add fine-grained hyperparameter search (Bayesian optimization).

License
This project is licensed under the MIT License.
Feel free to reuse and adapt for your own analyses!

python
Copy
Edit

---

### Doc-String Guidelines for `src/` Modules

For any Python files (e.g. `src/data_collection.py`), include at the top and for each function:

```python
"""
data_collection.py

Functions to scrape Reddit posts for Samsung Fold series using PRAW.
"""

import praw
import pandas as pd

def scrape_reddit(version_query: str,
                  version_label: str,
                  subreddits: list[str],
                  limit: int = 200) -> pd.DataFrame:
    """
    Fetch up to `limit` posts for each subreddit matching `version_query`.

    Parameters
    ----------
    version_query : str
        Search string (e.g., "Fold 7 OR Galaxy Fold 7").
    version_label : str
        Label to tag each row (e.g., "Fold 7").
    subreddits : list[str]
        List of subreddit names to search.
    limit : int, default=200
        Max number of posts per subreddit.

    Returns
    -------
    pandas.DataFrame
        DataFrame with columns: Version, Subreddit, Title, Body, Score, Comments, Timestamp, URL.
    """
    # function body...
