# Value-at-Risk Analysis

Hylo employs [**Value at Risk (VaR)**](https://www.investopedia.com/terms/v/var.asp) analysis to set appropriate thresholds for its risk management metrics. VaR is a statistical technique used to measure and quantify the level of financial risk within the system over a specific time frame.

Our model utilizes comprehensive SOL price data spanning from April 10, 2020, to August 15, 2024. This extensive dataset allows for a robust analysis of potential price movements.

### VaR for System CR and Threshold

#### Parameters

* **Data range:** April 10, 2020, to August 15, 2024
* **Confidence level:** 99.9% (representing a 0.1% probability event)
* **Time frame:** 1 day

#### Results and Threshold Setting

The analysis reveals a 99.9% VaR of -32.95% for a one-day price drop in SOL. Based on this, Hylo has set the minimum System CR threshold at 150%. This threshold ensures that the system can withstand a price drop corresponding to the 0.1% worst day in SOL's recent history without taking any action.

#### Justification for 150% Threshold

This threshold aims to:

1. Safeguard the system against rare but severe price drops, where the probability of a destabilizing event rises above 0.1%
2. Provide ample time for the protocol to act before reaching dangerously low collateralization levels
3. Maintain a conservative stance given SOL's observed market behavior

### VaR for Adjusted CR

For the Adjusted CR, Hylo uses a longer-term risk assessment based on a 31 days period.

#### Parameters

* **Data range:** April 10, 2020, to August 15, 2024
* **Confidence level:** 99.9% (representing a 0.1% probability event)
* **Time frame:** 31 days

#### Results

This analysis shows a 99.9% VaR of -56.82% for a 31-day price drop in SOL. Based on this calculation, Hylo considers the Adjusted Collateral Ratio healthy if it remains above 230%.

This higher threshold ensures that Hylo can absorb a 1-month price drawdown corresponding to the 0.1% worst month of SOL by activating all of its mechanisms without requiring direct action from users. The main action taken to address this metric is through incentives, primarily stability pool rewards. If we see this metric declining too much, we may increase the rewards distributed to stability pool LP to make it more attractive.

The use of different time frames (1-day for System CR, 31-day for Adjusted CR) allows Hylo to manage both short-term volatility and longer-term market trends effectively.

### VaR Trend Analysis

Our analysis shows a trend of decreasing VaR for a 1-day period for SOL year over year:

* Full dataset (2020-04-10 to 2024-08-15): 99.9% VaR of -32.95%
* Last 2 years: 99.9% VaR of -28.18%
* Last year: 99.9% VaR of -27.55%

Despite this trend suggesting a maturing market with potentially lower risk, we maintain the 150% threshold for the stability mode activation based on the full historical dataset for comprehensive risk coverage, prudent risk management, and user confidence.

Regular reviews of both the System CR and Adjusted CR thresholds will be conducted, with potential future adjustments carefully evaluated to balance robust risk management with capital efficiency.
