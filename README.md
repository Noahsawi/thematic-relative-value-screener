# Systematic Thematic Relative Value Screener

## Executive Summary
This repository contains a quantitative equity screening algorithm designed to identify asymmetric mean-reversion setups within the Nasdaq 100. 

Instead of evaluating equities against a single broad market index, this model employs a Multi-Thematic Regression Approach. It systematically evaluates stocks against highly correlated thematic sector ETFs (e.g., Semiconductors, Artificial Intelligence, Cloud Computing, Disruptive Innovation). The goal is to isolate true, stock-specific statistical dislocations (unjustified sell-offs) from general macro-driven sector drawdowns.

## Methodology & Scoring Matrix
The algorithm filters equities through a rigorous 5-factor scoring matrix. A stock is only flagged as a "High Probability Setup" if it demonstrates massive signal confluence, scoring at least a 4 out of 5 across multiple thematic comparisons.

1. Statistical Edge (Event Study / CAR): Calculates Cumulative Abnormal Returns via Ordinary Least Squares (OLS) regression against thematic benchmarks to find statistically unjustified price drops.
2. Momentum Exhaustion (RSI): Identifies panic-selling levels using a vectorized 14-day Relative Strength Index (< 35).
3. Macro Trend Dislocation (SMA 200): Measures extreme deviations from the 200-day moving average to gauge long-term mean-reversion potential.
4. Short-Term Momentum (MACD): Scans for positive histogram values (EMA12 > EMA26) to ensure the "falling knife" has started to catch support.
5. Relative Peer Performance: Directly benchmarks the asset's compounded return against the thematic ETF during the specific event window.

## Recent Findings (Case Study)
During recent tech market volatility, the screener successfully identified a severe, systematic anomaly within the Cybersecurity and Cloud SaaS sectors. 
Equities such as CRWD (CrowdStrike), PANW (Palo Alto Networks), ZS (Zscaler), and TEAM (Atlassian) triggered high-conviction signals (Score 4/5) across nearly all thematic benchmarks (BigTech, Cloud, Disruptive Innovation). The model mathematically proved that this specific sub-sector was sold off far more aggressively than broader tech or AI indices would justify, presenting a classic relative-value arbitrage opportunity.

## Tech Stack & Usage
* Python (Core Logic via Jupyter Notebook)
* Pandas & NumPy (Vectorized data manipulation for high-performance screening)
* Statsmodels (Econometric modeling & OLS regressions)
* yfinance (Automated bulk-downloading of market data)

Note: The script utilizes an efficient bulk-download architecture and inner join alignments to handle dirty data, trading halts, and timezone discrepancies without crashing.

**How to view and run:**
1. You can view the code and its latest screening output directly here on GitHub by opening the `.ipynb` file.
2. To run it locally, clone the repository, install the dependencies (`pip install -r requirements.txt`), and execute the cells in Jupyter Notebook, JupyterLab, or VS Code.

## Compliance & Data Note
To ensure full reproducibility, adherence to non-commercial data licensing, and public verifiability, this project utilizes open-source APIs (yfinance) rather than proprietary institutional data terminals (e.g., Bloomberg, LSEG Workspace).

## Disclaimer (Not Financial Advice)
The code, data, and opinions provided in this repository are strictly for educational, informational, and academic purposes only. They do not constitute financial, investment, or trading advice. Algorithmic trading involves substantial risk of loss and is not suitable for every investor. The creator of this repository assumes no responsibility or liability for any financial losses, damages, or errors resulting from the use of this code. Always conduct your own due diligence or consult a certified financial advisor before making any investment decisions.
