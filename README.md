# Value at Risk— Historical, Parametric & Monte Carlo Method with Backtesting
Excel-based VaR project that pulls 1-year daily prices (AAPL, GLD, BTC), normalizes, builds portfolio returns, computes VaR (Historical / Parametric / Monte Carlo), and performs backtesting (Kupiec POF). Focus on automation (Power Query), reproducibility, and explainable finance.
The goal is to measure portfolio risk, evaluate model reliability, and demonstrate applied risk analytics skills.

## Background

   - In real-world portfolio management, risk is just as important as return. Asset managers, banks, and hedge funds must continuously monitor the potential downside of their portfolios to comply with regulatory capital requirements (Basel III/IV), set risk limits, and design hedging strategies.
   - This project replicates the same risk analytics that financial institutions use by applying Value at Risk (VaR) models on a diversified $1M portfolio (30% Apple, 40% Gold, 30% Bitcoin).
      - Apple (AAPL) represents equity exposure.
      - Gold (GLD) serves as a defensive commodity hedge.
      - Bitcoin (BTC) captures high-volatility alternative assets.
   - By quantifying “how much can I lose in one day with 95% or 99% confidence?”, and backtesting the models for reliability, this project bridges the gap between academic risk theory and practical decision-making.

## Questions to Analyze

1) How large is my portfolio’s one-day downside risk?
   - Why it matters: Quantifies potential loss in a single trading day so risk limits, capital buffers, and stop-loss rules can be set.
   - How I answer it: Compute 1-day VaR at 95% and 99% using Historical, Parametric (Variance-Covariance), and Monte Carlo methods.
   - Key metrics: VaR (dollar and %), CVaR, comparative table of VaR by method, and time series of rolling VaR.

2) Are the VaR models statistically reliable for this portfolio?
   - Why it matters: A VaR number is useless if it under- or over-estimates real losses — model validation prevents false security.
   - How I answer it: Backtest VaR with Kupiec’s POF (frequency) test, compare observed vs expected exceptions, and compute p-values.
   - Key metrics: Number of exceptions (x), sample size (n), observed exception rate (p̂), LR statistic, p-value, and pass/fail decision per method.
  
## Dataset 

### Source

   - Daily returns from Stooq, a website that provides a wide range of historical financial data [Go to stooq](https://stooq.com/)

### Timeframe

   - 248 trading days (≈ 1 year).

### Portfolio Assumptions

   - The portfolio analyzed is valued at USD 1 million, allocated as follows: 30% Apple, 40% Gold, 30% Bitcoin.

## Reproducibility and Automation

### Data Pipeline

   - Parameterized function [fnGetStooq1Y](code/fnGetStooq1Y.pq) downloads CSV, promotes headers, renames, converts types, filters last 1 year.
   - Create tickers for stocks [Apple](code/AAPL.US), [Bitcoin](code/BTCUSD), [Gold](code/XAUUSD) to load in the table.
   - It makes data reproducible, single-click refresh; avoids manual CSV downloads.

### Data Handling
   - To align trading calendars (stock vs 24/7 crypto) and avoid errors due to missing values, the Excel function =IFERROR(stock,"") was used.


### Compute returns

   - Daily simple returns: stock_return = Close_t / Close_{t-1} - 1
   - Excel formula: stock return =IFERROR(BTCUSD[@Close]/BTCUSD!B2-1,"")


### Portfolio returns

   - Weighted sum: R_p,t = w1*r1,t + w2*r2,t + w3*r3,t
   - Calculated portfolio return w the excel function =SUMPRODUCT(B3:D3,$J$2:$L$2)

## Methodology

The project computes 1-day portfolio VaR at 95% and 99% confidence using three industry-standard approaches:
1. Historical Simulation
   - Uses actual past portfolio returns.
   - No distributional assumptions (non-parametric).
   - Steps:
      -   
      


 

