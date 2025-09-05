# Value at Risk— Historical, Parametric & Monte Carlo Method with Backtesting
Excel-based VaR project that pulls 1-year daily prices (AAPL, GLD, BTC), normalizes, builds portfolio returns, computes VaR (Historical / Parametric / Monte Carlo), and performs backtesting (Kupiec POF). Focus on automation (Power Query), reproducibility, and explainable finance.
The goal is to measure portfolio risk, evaluate model reliability, and demonstrate applied risk analytics skills.

### Questions to Analyze

1) How large is my portfolio’s one-day downside risk?
   - Why it matters: Quantifies potential loss in a single trading day so risk limits, capital buffers, and stop-loss rules can be set.
   - How I answer it: Compute 1-day VaR at 95% and 99% using Historical, Parametric (Variance-Covariance), and Monte Carlo methods.
   - Key metrics: VaR (dollar and %), CVaR, comparative table of VaR by method, and time series of rolling VaR.

2) Are the VaR models statistically reliable for this portfolio?
   - Why it matters: A VaR number is useless if it under- or over-estimates real losses — model validation prevents false security.
   - How I answer it: Backtest VaR with Kupiec’s POF (frequency) test, compare observed vs expected exceptions, and compute p-values.
   - Key metrics: Number of exceptions (x), sample size (n), observed exception rate (p̂), LR statistic, p-value, and pass/fail decision per method.
  
## Dataset and reproducibility

   - Source: Daily returns from Stooq, a website that provides a wide range of free historical financial data [Go to stooq](https://stooq.com/)
   - Timeframe: 248 trading days (≈ 1 year).
     
### Data Pipeline

1) Data ingestion (Power Query)
   - Parameterized function [fnGetStooq1Y] (code/fnGetStooq1Y.pq) downloads CSV, promotes headers, renames, converts types, filters last 1 year.
   - Create tickers = fnGetStooq_1Y("AAPL.US"), = fnGetStooq_1Y("XAUUSD"), = fnGetStooq_1Y("BTCUSD") to load stocks in the table.
   - It makes data reproducible, single-click refresh; avoids manual CSV downloads.


