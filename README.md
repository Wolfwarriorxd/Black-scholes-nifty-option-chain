# Black–Scholes Validation on NSE NIFTY Options

## Overview
This project presents a cross-sectional validation of the Black–Scholes option pricing model using a single-day NSE NIFTY option-chain snapshot.  
The objective is to evaluate how well Black–Scholes performs when its assumptions are enforced on real market data, rather than optimizing the model to fit prices.

Volatility is calibrated using at-the-money (ATM) implied volatility, and pricing errors across strikes are analyzed to quantify model misspecification due to the volatility smile.

## Data Description
- Source: Official NSE option-chain Excel snapshot
- Underlying: NIFTY index options
- Expiry: Nearest monthly expiry
- Frequency: Single trading day (cross-sectional data)
- Option price used: Bid–Ask midpoint (fallback to LTP when unavailable)

Spot price is treated as an external scalar input.

## Methodology
1. Load and clean NSE option-chain Excel data
2. Compute implied volatility for each option using the Black–Scholes formula
3. Identify ATM options based on moneyness
4. Estimate ATM implied volatility using the median of ATM IVs
5. Price all options using Black–Scholes with constant ATM volatility
6. Evaluate pricing errors across strikes
7. Visualize implied volatility smile and pricing error patterns

This approach enforces the constant-volatility assumption intrinsic to Black–Scholes, avoiding trivial zero-error identities.

## Results Summary
- ATM Implied Volatility: approximately 15%
- Mean Absolute Error (MAE): approximately ₹100
- Root Mean Squared Error (RMSE): approximately ₹140

Pricing errors increase systematically away from the ATM region, indicating the presence of a pronounced volatility skew in NIFTY options.

## Diagnostics

### Implied Volatility Smile
The implied volatility smile shows elevated volatility for deep out-of-the-money puts and a rising volatility profile for out-of-the-money calls, violating the constant-volatility assumption of Black–Scholes.


### Pricing Error vs Moneyness
Pricing errors grow as options move further away from ATM, consistent with model misspecification rather than random noise.


## Interpretation
- Black–Scholes performs reasonably near the ATM region
- Constant volatility fails to capture skew and tail risk pricing
- Observed errors are structural and reflect known limitations of the model

This analysis mirrors how volatility models are evaluated in practice by quantitative traders and risk teams.

## Limitations
- European exercise assumption
- No dividends
- Single maturity
- No stochastic volatility
