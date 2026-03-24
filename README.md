# EURUSD-2025-backtest
*A systematic implementation of discretionary liquidity concepts in FX trading*

---

## 1. Overview

This project implements and evaluates my current **rule-based intraday trading strategy** on EUR/USD using 5-minute data.

The strategy translates discretionary price action concepts — including:
- Liquidity sweeps  
- Fair Value Gaps (FVG)  
- Market Structure Shifts (MSS)  

— into a **systematic backtesting framework**.

The objective is to determine whether these concepts can produce **consistent, risk-adjusted returns** under strict execution and risk management constraints.

---

## 2. Strategy Logic

The strategy follows a structured **intraday liquidity framework**:

### 2.1 Session Model

- **Asian Session (Accumulation)**  
  Defines the initial range (high / low)

- **London Session (Manipulation)**  
  Price sweeps liquidity above/below Asian range

- **New York Session (Distribution)**  
  Continuation or reversal toward opposing liquidity

---

### 2.2 Entry Conditions

A trade is executed only when all conditions are met:

1. **Liquidity Sweep**
   - Price sweeps Asian high/low during London session  

2. **Higher Timeframe Context**
   - Sweep occurs into a higher timeframe Fair Value Gap (FVG)  

3. **Market Structure Shift (MSS)**
   - Confirmed break in short-term structure (5M / 15M)  

4. **Execution**
   - Entry at **0.618 retracement** of the impulse leg  

---

### 2.3 Exit Rules

- **Take Profit**:  
  Opposing liquidity (Asian range or higher timeframe imbalance)

- **Stop Loss**:  
  Beyond liquidity sweep  

- **Execution Model**:  
  Uses **bid/ask prices** to simulate realistic fills  

---

## 3. Data

- **Source**: Dukascopy EUR/USD tick-derived data  
- **Frequency**: 5-minute bars  
- **Period**: January 2025 – December 2025  

### Fields:
- Bid/Ask OHLC  
- Volume  
- Derived:
  - Mid-price  
  - Spread  

---

## 4. Backtest Assumptions

- Fixed risk per trade: **0.50% of starting equity**  
- No slippage beyond bid/ask spread  
- Orders executed at next available price  
- No latency modelling  
- Single-position exposure (no stacking)  

---

## 5. Performance Metrics

The strategy is evaluated using:

- Sharpe Ratio  
- Maximum Drawdown  
- Win Rate  
- Expectancy (R-multiple)  
- Payoff Ratio  

---

## 6. Results
- You may refer to the quantstats report for a detailed analysis of the results.
  
| Metric            | Value   |
|------------------|--------|
| Sharpe Ratio     | 2.06   |
| Max Drawdown     | -8.0%  |
| Win Rate         | 46%    |
| Expectancy       | 0.151 R |

---

## 7. Key Insights

- Performance is highly dependent on **session-based volatility expansion**  

- Drawdowns cluster during:
  - Low-volatility environments (EUR/USD compression)  
  - Strong directional momentum (macro-driven moves)  

- Strategy edge is strongest during:
  - London session liquidity sweeps  
  - Short-term mean reversion after displacement  

These findings led to the development of a **volatility regime filter**, which dynamically adjusts:
- Trade frequency  
- Position sizing  

---

## 8. Limitations

- No transaction cost modelling beyond spread  
- No slippage or execution latency  
- Simplified FVG and MSS detection logic  
- No macroeconomic event filtering (e.g. FOMC, NFP)  

---

## 9. Future Improvements

- Integrate volatility regime filter for adaptive sizing  
- Add event risk filter (exclude high-impact news)  
- Expand to multi-asset framework (EUR/USD + Gold)  
- Improve execution modelling (slippage + latency) 

How to Run
1. Install dependencies
pip install -r requirements.txt

2. Prepare data
Place the following files in the working directory:

- EURUSD_5 Mins_Bid_2025.csv
- EURUSD_5 Mins_Ask_2025.csv

3. Run backtest
python eurusd_backtest_clean.py

Author

Alden Lee
FX Trader | Quantitative Strategy Development | Risk-Focused Execution

Focus: EUR/USD & Gold intraday trading
Approach: Discretionary framework with systematic overlays
Goal: Transition toward institutional trading and hedge fund strategy development
