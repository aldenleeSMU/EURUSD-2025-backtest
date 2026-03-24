# EURUSD-2025-backtest
EUR/USD Intraday Strategy Backtest (2025)
Overview

This project implements and evaluates a rule-based intraday FX trading strategy on EUR/USD using 5-minute data. The strategy is derived from discretionary price action concepts (liquidity sweeps, fair value gaps, and market structure shifts) and translated into a systematic backtesting framework.

The objective is to assess whether these concepts can generate consistent, risk-adjusted returns under strict execution and risk management rules.

Strategy Logic

The strategy follows a structured intraday liquidity framework:

1. Session Framework
- Asian Session (Accumulation): Defines the initial range (high/low)
- London Session (Manipulation): Price sweeps liquidity above/below Asian range
- New York Session (Distribution): Continuation or reversal toward opposing liquidity

2. Entry Conditions

A trade is triggered when all of the following conditions are met:

- Liquidity Sweep
- Price sweeps Asian high/low during London session
- Higher Timeframe Context
- Sweep occurs into a higher timeframe Fair Value Gap (FVG)
- Market Structure Shift (MSS)
- Confirmed break in short-term structure (5M / 15M)
Entry
- Executed at 0.618 retracement of the impulse leg

3. Exit Rules
- Take Profit: Opposing liquidity (Asian range or HTF imbalance)
- Stop Loss: Beyond liquidity sweep
- Execution: Uses bid/ask prices to simulate realistic fills

Data
- Source: Dukascopy EUR/USD tick-derived 5-minute data
- Period: January 2025 – December 2025
- Fields:
-   Bid/Ask OHLC, Volume
- Mid-price and spread constructed from bid/ask series

Backtest Assumptions
- Fixed risk per trade (configurable)
- No slippage beyond bid/ask spread
- Orders executed at next available price
- No latency modelling
- Single-position exposure (no stacking)

Performance Metrics

The backtest evaluates:
- Sharpe Ratio
- Maximum Drawdown
- Win Rate
- Expectancy (R-multiple)
- Payoff Ratio
- Results



Metric	Value
- Sharpe Ratio	2.06
- Max Drawdown	-8.0%
- Win Rate	46%
- Expectancy	0.151 R

Key Insights
- Strategy performance is highly dependent on session-based volatility expansion
- Drawdowns tend to cluster during:
- Low volatility environments (EUR/USD compression)
- Strong directional momentum (particularly during macro-driven moves)
The edge is strongest during:
- London session liquidity sweeps
- Short-term mean reversion following displacement

These findings motivated the development of a volatility regime filter, which dynamically adjusts trade frequency and position sizing.

Limitations
- No transaction cost modelling beyond spread
- No slippage or execution latency
- FVG and MSS detection simplified for systematic implementation
- Strategy does not incorporate macroeconomic event filtering (e.g. FOMC, NFP)

Future Improvements
- Integrate volatility regime filter for adaptive position sizing
- Add event risk filter (exclude high-impact news periods)
- Introduce portfolio context (EUR/USD + Gold interaction)
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
