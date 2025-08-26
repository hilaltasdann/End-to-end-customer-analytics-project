# End-to-end-customer-analytics-project

# Customer Analytics Suite – CLTV, RFM & Segmentation (with Streamlit)

An end-to-end customer analytics project for retail/e-commerce featuring:

Probabilistic CLTV (BG/NBD + Gamma-Gamma, weekly)

RFM segmentation with actionable segments

Unsupervised clustering (K-Means & Hierarchical)

Streamlit dashboard for quick exploration

This repo is built from FLO’s omnichannel dataset exercises and briefs (project/story, variables, and steps) and consolidated into a single codebase for reproducibility and publication. 
 

# What’s inside

CLTV (6-month) using Beta-Geo (BG/NBD) for purchase frequency and Gamma-Gamma for monetary value; plus 3- and 6-month expected sales.

RFM scores (recency, frequency, monetary), RF/RFM strings and business-friendly segments (e.g., champions, loyal_customers).

Customer clustering with feature scaling, elbow plot, and dendrograms.

Segment summaries & CSV exports for campaigns.

# Dataset

flo_data_20k.csv (19,945 customers, omnichannel behavior; 2020–2021). Fields include order counts/values online & offline, first/last order dates, channels, and interested categories. (See briefs/scripts above for details.)


- clone & enter
git clone https://github.com/<you>/customer-analytics-suite.git
cd customer-analytics-suite

- create & activate env (recommended)
python -m venv .venv

- mac/linux
source .venv/bin/activate

- windows (powershell)
.venv\Scripts\Activate.ps1

- install deps
pip install -r requirements.txt

- place the dataset
mkdir -p data && mv /path/to/flo_data_20k.csv data/

- run Streamlit app
streamlit run streamlit_app/app.py

# How it works (modules)

src/cltv_bg_gammadist.py

Builds probabilistic CLTV: caps outliers, creates totals, converts dates, computes recency/T in weeks, fits BG/NBD and Gamma-Gamma, predicts 3/6-month expected sales and 6-month CLTV, then quartiles into A/B/C/D segments. (Consolidated from your original CLTV script & brief.) 
 

src/rfm.py
Calculates RFM metrics, converts to scores (1–5), builds RF/RFM strings, and maps to segments (champions, loyal_customers, etc.) as in your spec. 
 

src/clustering.py
Creates modeling features (order counts/values, recency, tenure), log-transforms, scales, runs K-Means (with elbow) and Agglomerative clustering (with dendrogram). 

streamlit_app/app.py
Simple UI to run the pipeline on the local CSV and preview CLTV table, RFM segments, and clustering summaries.

# Outputs

cltv.parquet/csv – predicted CLTV, exp_sales_3_month, exp_sales_6_month, exp_average_value, and cltv_segment.

rfm.parquet/csv – RFM metrics, scores, RF/RFM strings, segment.

clusters.parquet/csv – Segment labels + feature stats.

# Tech stack

Pandas, NumPy, scikit-learn, lifetimes, Matplotlib, Seaborn, Streamlit, SciPy, Yellowbrick.
(Optionally: XGBoost/LightGBM/CatBoost for ML add-ons.)

# License & attribution

This repo consolidates your original FLO exercises/briefs and code into a single, reusable project. Please keep dataset terms and original attributions as needed. 

3) requirements.txt
pandas>=2.0
numpy>=1.24
scikit-learn>=1.3
scipy>=1.10
matplotlib>=3.7
seaborn>=0.13
streamlit>=1.34
lifelines==0.27.8
lifetimes==0.11.3
yellowbrick>=1.5
pyarrow>=14.0



