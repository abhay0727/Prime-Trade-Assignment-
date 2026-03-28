# Data Science Intern Project: Trader Behavior vs. Market Sentiment

This repository contains the solution for the PrimeTrade Data Science Intern assignment. The objective is to analyze the relationship between automated trader behavior on Hyperliquid (a decentralized perpetuals exchange) and the general Bitcoin market sentiment (Fear & Greed Index).

## Project Structure
```text
PrimeTrade/
│
├── sentiment.csv                   # Daily Bitcoin Fear & Greed Index data
├── trader_data.csv                 # Raw transaction-level trader data
│
├── download.py                     # Programmatic data fetching script (Google Drive)
├── analysis.py                     # Standalone Python script for robust initial analysis (Part A)
├── build_notebook.py               # Generator script for the Jupyter notebook
│
├── outputs/                        # Folder containing analytical outputs and charts
│   └── daily_trader_metrics.csv    # Transformed Part A features exported
│
├── Trader_Analysis_Final.ipynb     # The final comprehensive Jupyter Notebook (Option 1 Deliverable)
└── README.md                       # This instruction file
```

## Setup & Running the Analysis

**1. Create & Activate Virtual Environment:**
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On MacOS/Linux:
source venv/bin/activate
```

**2. Install Dependencies:**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter gdown nbformat
```

**3. Data Acquisition (Optional, data already provided locally):**
```bash
python download.py
```
*(This gracefully handles downloading from Google Drive using gdown).*

**4. Execute the Jupyter Notebook (Primary Deliverable):**
```bash
jupyter notebook Trader_Analysis_Final.ipynb
```
From the Jupyter UI, click **"Run All"** to execute the pipeline. The notebook covers:
*   **Part A:** Merging datasets, fixing timestamps, extracting features (PnL, Volume proxy for Leverage, Win Rates).
*   **Part B:** Segmenting groups by sentiment (Fear vs. Greed) and applying statistical t-tests to evaluate position sizing and profitability changes.
*   **Part C & Bonus:** Running Unsupervised ML (PCA and K-Means Clustering) to discover behavioral archetypes to provide actionable, concrete copy-trading strategies.

## Notes & Assumptions
*   **Missing 'Leverage' Field:** The assignment description stated the availability of a 'leverage' field. This field is absent from the provided `trader_data.csv`. We have successfully substituted 'Total Trading Volume ($ USD)' and 'Avg_Trade_Size' as proxies for leverage to fulfill the requirements.
*   The sentiment scale uses `value > 50` as Greed, and `value <= 50` as Fear for binary classification tests.
