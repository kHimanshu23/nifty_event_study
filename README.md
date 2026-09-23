# NIFTY Event Study — Post-Fall Recovery Analysis

## 1. Project Overview

This project investigates the hypothesis:

> **“After a significant one-day fall in NIFTY, the market tends to recover over the next few trading days.”**

The study examines NIFTY's forward returns after significant one-day falls over **1-day, 3-day and 5-day holding periods**.

The analysis includes event detection, forward-return analysis, comparison with a normal-market baseline, statistical testing, bootstrap analysis, threshold robustness, out-of-sample analysis, event clustering, transaction-cost analysis and a simple event-driven backtest.

---

## 2. Methodology

### Event Definition

A significant fall is defined as:

**Daily Return ≤ −3.0%**

Daily return is calculated as:

**Daily Return = (Closeₜ / Closeₜ₋₁ − 1) × 100**

### Entry

Entry is assumed at the **Open of the next trading day** after the event.

This avoids look-ahead bias because the event-day return is known only after the trading day has ended.

### Holding Period

The study evaluates:

* 1 trading day
* 3 trading days
* 5 trading days

### Exit

The position is exited at the **Close** after the selected holding period.

### Baseline

Event-period forward returns are compared with forward returns from normal, non-event NIFTY trading days over the same period.

The baseline is used to determine whether post-fall performance is different from normal market behaviour.

### Statistical Analysis

The analysis includes:

* Mean return
* Median return
* Win rate
* Standard deviation
* 95% confidence intervals
* Hypothesis testing
* Bootstrap confidence intervals

### Robustness

The event threshold was tested at:

* −2.0%
* −2.5%
* −3.0%
* −3.5%
* −4.0%

The results were evaluated across 1D, 3D and 5D holding periods.

### Out-of-Sample Analysis

The data was split into a development period and an out-of-sample period.

**Split date: 10 July 2024**

The out-of-sample results were evaluated separately from the development period.

### Event Clustering

The gap between significant-fall events was examined to assess whether closely occurring events could create dependence between observations.

### Transaction Costs and Slippage

A total round-trip assumption of **0.20%** was used:

* 0.10% transaction cost
* 0.10% slippage

---

## 3. Data Source

The analysis uses historical daily NIFTY data containing:

* Date
* Open
* High
* Low
* Close

### Data Coverage

**Start:** 22 September 2015
**End:** 18 September 2026
**Total observations:** 2,722

### Data Validation

The dataset was checked for:

* Missing dates
* Duplicate dates
* Incorrect date ordering
* Missing or invalid OHLC values
* Suspicious observations
* Actual date coverage

The dataset was cleaned and validated before conducting the event analysis.

---

## 4. Project Structure

```text
NIFTY-Event-Study/
│
├── README.md
│
└── [analysis files]
```

The repository contains the Python/Jupyter analysis used to perform the event study.

---

## 5. Assumptions

1. The NIFTY daily OHLC data is sufficiently accurate for the analysis.
2. An event is identified using information available after the event trading day has ended.
3. Entry occurs at the next trading day's Open.
4. Forward returns are calculated using trading days rather than calendar days.
5. Normal non-event trading days are used as the baseline.
6. Closely occurring events may not be completely independent, so event gaps are examined.
7. Transaction costs and slippage are considered separately from gross returns.
8. Historical results do not guarantee future market behaviour.

---

## 6. Limitations

### Sample Size

Large one-day NIFTY falls are relatively infrequent, resulting in a smaller event sample than the total dataset.

### Market Regimes

The dataset covers different market environments. The relationship may vary across different market regimes.

### Parameter Sensitivity

Results can change when the event threshold or holding period changes. Testing multiple thresholds and horizons also creates a risk of data snooping and multiple-testing effects.

### Out-of-Sample Sample Size

The out-of-sample period contains only a small number of events, limiting the strength of independent validation.

### Event Dependence

Closely occurring events may be related to the same market episode and may therefore not be fully independent observations.

### Transaction Costs

Actual execution costs and slippage can differ from the assumptions used in the analysis.

### Historical Relationship

A relationship observed in historical NIFTY data does not guarantee that the same behaviour will occur in the future.

---

## 7. Reproducibility

The analysis uses a defined event threshold, entry rule, holding periods and statistical methodology so that the research can be reproduced using the same NIFTY dataset.

The event threshold and holding periods are configurable within the analysis, allowing alternative specifications to be tested without changing the overall research logic.

