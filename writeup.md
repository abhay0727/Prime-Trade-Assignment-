# Trader Behavior vs. Market Sentiment: Executive Summary

This write-up summarizes the methodology, insights, and actionable strategy recommendations derived from analyzing trader behavior on the Hyperliquid decentralized exchange against the daily Bitcoin Fear & Greed Index.

---

## 1. Methodology

**Data Preparation:**
*   Merged continuous transaction-level trader data (`trader_data.csv`) with daily Bitcoin sentiment data (`sentiment.csv`) on a standardized daily timeframe.
*   **Feature Engineering:** Calculated daily account metrics, including Win Rate, Average Trade Size, Total Trading Volume, and Daily PnL. Since the `leverage` column was absent from the dataset, Total Trading Volume and Average Trade Size were utilized as proxy metrics for trader aggressiveness and position sizing.
*   **Sentiment Segmentation:** Market sentiment was binarized into "Greed" (Index > 50) and "Fear" (Index $\leq$ 50) for direct A/B statistical comparisons.

**Analytical Approach:**
*   **Hypothesis Testing:** Conducted Welch’s t-tests (two-sample, unequal variance) to determine if distributions of daily PnL and trade sizing differed significantly between Fear and Greed regimes.
*   **Behavioral Archetyping:** Grouped lifetime trader profiles (spanning Lifetime PnL, Win Rate, and Average Daily Volume) using Unsupervised Machine Learning. 
    *   Applied **Principal Component Analysis (PCA)** to reduce dimensionality.
    *   Applied **K-Means Clustering (K=3)** to categorize traders into distinct behavioral archetypes automatically based on empirical data rather than arbitrary thresholds.

---

## 2. Key Insights

1. **Volume Surges During Extreme Sentiment:** Average daily trading volumes per trader increase drastically during "Extreme Greed" days. This suggests an influx of retail momentum trading or traders expanding their position sizes preemptively, acting on market FOMO (Fear of Missing Out).
2. **Profitability Disconnect:** Despite higher trading volumes during Greed regimes, Win Rates often plateau or slightly decay. Overtrading and high transaction fees (friction) tend to erode capital when the market is overextended.
3. **Distinct Behavioral Archetypes:** The K-Means clustering algorithm identified three primary groups of traders:
    *   **Archetype A (Retail / High-Frequency):** Characterized by high daily trade counts, lower average trade sizes, and near 50% (or lower) win rates. Highly susceptible to sudden market sentiment shifts.
    *   **Archetype B (Snipers / Whales):** Low trade frequency but massive average trade sizes and significantly higher long-term Win Rates. These traders are largely neutral to daily index fluctuations and pick systematic entries.
    *   **Archetype C (Momentum Scalpers):** Moderate trade frequency and sizing, performing best specifically when the index transitions from Fear to Greed.

---

## 3. Actionable Strategy Recommendations

Based on the quantitative insights gathered, the following data-backed trading strategies are proposed:

### A. Market-Regime Position Sizing
*   **Strategy:** Implement a dynamic risk-multiplier based on the Fear & Greed Index.
*   **Execution:** 
    *   When the Index enters **Extreme Greed ($>80$)**, automatically scale down open position sizes or new entries by 20-30%. This preserves capital from impending mean-reversion pullbacks. 
    *   Conversely, allocate higher capital percentages to long swing positions when the Index hits **Extreme Fear ($<20$)**, historically a zone where "Sniper" archetypes accumulate their largest, most profitable positions.

### B. Archetype Mimicry (Smart-Money Copy Trading)
*   **Strategy:** Utilize the K-Means cluster labels to build a filtered signal-aggregation engine.
*   **Execution:** Completely ignore the order flow from "Archetype A" (Retail). Design an automated copy-trading algorithm that strictly assigns high trust weights to the trades executed by "Archetype B" (Snipers/Whales). This system limits overtrading and effectively mimics the most consistently profitable cohort on the exchange, bypassing emotional market noise.
