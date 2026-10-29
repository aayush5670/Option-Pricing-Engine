# Option Pricing & Monte Carlo Simulation

This repository contains a Jupyter Notebook implementing option pricing models for the Nifty 50 Index (`^NSEI`). It calculates theoretical prices for European Call and Put options using both analytical and numerical simulation methods.

## Features

- **Historical Data Retrieval**: Automatically fetches historical daily adjusted close prices for the Nifty 50 index using the `yfinance` API.
- **Parametric Estimation**:
  - Daily log returns calculation.
  - Historical annualized volatility estimation based on trading days.
  - Continuously compounded risk-free rate and dividend yield modeling.
- **Black-Scholes-Merton Model**: Analytical evaluation of European Call and Put option prices accounting for continuous dividend yields.
- **Monte Carlo Simulation**:
  - Large-scale stochastic simulation of asset price paths at maturity using Geometric Brownian Motion (GBM).
  - Discounted payoff calculations for Call and Put options.
  - Standard error estimation for simulation accuracy.

## Prerequisites & Installation

Ensure you have Python 3.8+ installed along with the required dependencies:

```bash
pip install pandas numpy yfinance matplotlib scipy
```

## Methodology & Formulas

### 1. Black-Scholes Model

The pricing formulas for European options with a continuous dividend yield $q$ and risk-free rate $r$ are:

$$d_1 = \frac{\ln(S/K) + \left(r - q + \frac{1}{2}\sigma^2\right)T}{\sigma\sqrt{T}}$$

$$d_2 = d_1 - \sigma\sqrt{T}$$

- **Call Price ($C$)**: $C = S e^{-qT} N(d_1) - K e^{-rT} N(d_2)$
- **Put Price ($P$)**: $P = K e^{-rT} N(-d_2) - S e^{-qT} N(-d_1)$

### 2. Monte Carlo Simulation

Terminal stock prices $S_T$ are generated using the exact solution to the Geometric Brownian Motion SDE:

$$S_T = S_0 \exp\left( \left(r - q - \frac{1}{2}\sigma^2\right)T + \sigma \sqrt{T} Z \right)$$

where $Z \sim \mathcal{N}(0, 1)$.

Option payoffs are determined by taking the expectation of discounted terminal payoffs:
- $\text{Call Payoff} = e^{-rT} \max(S_T - K, 0)$
- $\text{Put Payoff} = e^{-rT} \max(K - S_T, 0)$

## Usage

Run the main notebook to execute the calculations:

```bash
jupyter notebook
```

Open and execute the cells sequentially in the provided notebook file to fetch updated ticker data and calculate option prices.
