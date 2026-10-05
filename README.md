# Quantitative Signal Detection & HMM Regime-Switching Strategy

A two-part quantitative investment framework designed to identify market signals between Nasdaq growth (`QQQ`), covered-call income (`JEPQ`), and Cash equivalents (`CASH`), utilizing a Hidden Markov Model (HMM) to dynamically allocate capital based on latent market regimes.

This project has also been published on my blog Hoops Hypothesis, in two parts:

1. https://hoops-hypothesis.blogspot.com/2026/06/jepq-vs-qqq-finding-signals-in-noise.html

2. https://hoops-hypothesis.blogspot.com/2026/09/dynamic-asset-allocation-via-hidden.html

## Framework Overview
### Part 1: Signal Detection (JEPQ vs. QQQ)

Before fitting structural models, Part 1 analyzes the empirical trade-offs, return distributions, and stationarity properties between QQQ (high beta/growth) and JEPQ (covered-call income/dampened volatility):

1. Feature Engineering: Evaluates log returns, Parkinson range volatility, and relative price ratios to isolate signal from market noise.

2. Stationarity & Distribution Verification: Confirms feature stationarity required for Gaussian HMM emission distributions.

### Part 2: HMM Regime Detection & Allocation
Part 2 leverages a 3-State Gaussian Hidden Markov Model trained on the engineered stationary features to infer underlying market regimes and drive dynamic portfolio shifts.

#### Key Technical Features

1. Zero Look-Ahead Bias: Enforces strict $1$-day execution shifts (shift(1)) so that decisions made at time $t$ using data up to $t$ drive trading returns earned across $t+1$.

2. Rolling-Window Inference: Uses a 60–120 day rolling feature buffer in the Forward Algorithm ($\pi_t$) to eliminate HMM "cold-start" initialization noise during daily execution.

3. Argmax Strategy (Hard Switching): Rebalances 100% of the portfolio into the single asset corresponding to the maximum predicted regime probability.

4. Standardized Return Accounting: Computes daily portfolio returns in simple arithmetic space ($R_t$) across blended assets before converting to log space ($\ln(1 + R_t)$), ensuring equitable performance comparisons against buy-and-hold benchmarks.

#### Performance Evaluation Metrics
Out-of-sample performance is evaluated across three standardized tracks:

1. Argmax Strategy (Dynamic Hard Regime Switching)

2. QQQ Buy & Hold (Growth Benchmark)

3. JEPQ Buy & Hold (Income Benchmark)

## Risk Disclaimers
This repository is built strictly for educational and research purposes. Backtested trading performance does not guarantee live market results. Financial markets carry substantial risk, and trading decisions should be evaluated against individual risk tolerance, execution slippage, and transaction fees.
