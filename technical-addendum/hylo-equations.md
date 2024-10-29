# Hylo Equations

### True LST value

For calculation purposes, both xSOL and hyUSD are priced using the pure SOL price. However, since they are backed by Liquid Staking Tokens (LSTs), we need to accurately capture the price of these LSTs at any time. Using the market price of LSTs could pose significant problems, especially during severe market volatility, when the peg of these LSTs can be lost due to lack of liquidity and also they have a greater susceptibility to manipulation compared to SOL prices. Therefore, we use the **Sanctum SOL value calculator program** to determine the true LST price based on the amount of SOL held in each LST stake pool.

The true price of an LST in SOL can be defined by the following equation:

$$
\text{True\_LST\_price} = \frac{\text{Amount\_of\_SOL\_in\_the\_stake\_pool}}{\text{Total\_LST\_supply}}
$$

### SOL/USD Oracle

To calculate the value of hyUSD in SOL, ensuring it remains pegged 1:1 with the USD, we need to have the SOL price. For this, we are using the **Pyth EMA SOL/USD** price oracle.

### Net Asset Value (NAV) calculation for hyUSD and xSOL

The Net Asset Value (NAV) defines how much both tokens are worth in SOL. Since the SOL price isn't stable, the NAV of hyUSD needs to be constantly adjusted according to the SOL price to maintain its 1:1 peg to the USD.

The **NAV of hyUSD in SOL** can be calculated using the following equation:

$$
\text{hyUSD\_SOL\_NAV} = \frac{1}{\text{SOL\_Price}}
$$

Based on the **hyUSD NAV in SOL**, we can then calculate the **NAV of xSOL in SOL** using this equation:

$$
\text{xSOL\_SOL\_NAV} = \frac{\text{Total\_SOL\_in\_reserve} - (\text{hyUSD\_NAV} \times \text{hyUSD\_supply})}{\text{xSOL\_supply}}
$$

### Collateral Ratio calculation

The Collateral Ratio is a metric indicating the health level of hyUSD. It is extremely important to track it accurately to activate stability modes when needed. The Collateral Ratio of hyUSD can be calculated using the following equation:

$$
\text{Collateral\_Ratio} = \frac{\text{Total\_SOL\_In\_Reserve}}{\text{hyUSD\_NAV\_In\_SOL} \times \text{hyUSD\_Supply}}
$$

### Stability pool APY calculation

The stability pool APY is variable and greatly depends on the percentage of SOL value being staked, the APY of the reserve, and the defined percentage of Revenue Distribution.&#x20;

The **percentage of staked SOL** can be calculated as follows:

$$
\%_{\text{staked\_SOL}} = \frac{\text{Total\_SOL\_in\_reserve}}{\text{hyUSD\_Staked\_Amount} \times \text{hyUSD\_NAV\_in\_SOL}}
$$

The **Average Reserve Yield** can be calculated as follows:

$$
\text{Average\_Reserve\_Yield} = \frac{ \sum_{i=1}^{x} (\text{Supply}_{\text{LST}_i} \times \text{Price}_{\text{LST}_i} \times \text{APY}_{\text{LST}_i}) }{\text{Total\_SOL\_In\_Reserve}}
$$

The percentage of Revenue Distribution is dynamically adapted to stay attractive. If the percentage of staked SOL is low, this percentage may be reduced to maximize treasury profit. During periods when it is high, it may be increased to remain competitive compared to other stablecoins yields.

With all of this then we can calculate the **stability pool APY** as follow:

$$
\text{APY} = \text{Average\_Reserve\_Yield} \times \%_{\text{revenue\_distribution}} \times \%_{\text{staked\_SOL}}
$$

### xSOL Effective Leverage

The xSOL effective leverage will change constantly. To calculate it, we first need to determine the **virtual xSOL market cap**. This can be calculated as follows:

$$
\text{Market\_Cap}_{\text{xSOL}} = \text{NAV}_{\text{xSOL}} \times \text{Supply}_{\text{xSOL}}
$$

Next, we calculate the x**SOL effective leverage** with this equation:

$$
\text{Effective\_Leverage}_{\text{xSOL}} = \frac{\text{Total\_SOL\_In\_Reserve}}{\text{Market\_Cap}_{\text{xSOL}}}
$$

The effective leverage will tend to exponentially increase as the collateral ratio gets closer to 100%, and will approach 1 (indicating it follows the SOL price perfectly) as the collateral ratio increases.
