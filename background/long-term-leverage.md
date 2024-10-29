# Long Term Leverage

Crypto traders love leverage, and one only needs to consider the revenue generated on trading platforms like [Jupiter](https://defillama.com/protocol/jupiter-perpetual-exchange#information), [Drift](https://defillama.com/protocol/drift#information), and [Kamino](https://defillama.com/protocol/kamino#information) to be convinced. Despite its "degen" reputation, leveraged trading plays a crucial role in DeFi, aiding in price discovery and accounting for a significant portion of volume on decentralized exchanges.

### Leverage Strategies and Their Drawbacks

The two dominant leverage strategies in the cryptocurrency market are perpetual futures and spot borrowing. While these methods differ in their mechanics, they share several significant drawbacks.

#### **Mechanics**

* **Perpetual Futures** (perps) allow traders to open leveraged long or short positions without an expiry date. In AMM-based perps, traders interact with a liquidity pool, compensating liquidity providers with a funding rate for open positions on the wrong side of the oracle price. In order book-based perps, traders' orders match against each other while funding rates align prices with the spot market. Both variants require collateral, and traders risk liquidation if the market price slips too far from their prediction.
* **Spot Leverage** allows a trader to borrow assets against collateral to increase their position size. One strategy may involve borrowing a stablecoin to purchase a volatile asset, hoping to profit from the spread of the asset's appreciation over a period of time. The trader then sells the volatile asset and uses the proceeds to repay the stablecoin loan with interest.

#### **Drawbacks**

* **High Ongoing Costs**
  * Perps traders pay an average annualized funding rate of [60% on Jupiter perpetual exchange](https://jup.ag/perps) and similar rates on other exchanges.
  * In spot leverage, USDC borrowing rates on lending platforms like [Kamino range between 10% to 40%](https://app.kamino.finance/lending/reserve/7u3HeHxYDLhnCoErrtycNokbQYbWGzLs6JSDqGAv5PfF/D6q6wuQSrifJKZYpR1M8R4YawnLDtDsMmWM1NbBmgJ59). This means that borrows must generate annualized returns greater than the lending rate to profit.
* **Liquidation Risk:** Both methods expose users to forced position closures (liquidation) in high volatility periods, often leading to significant losses.
* **Health Management:** Traders must either actively monitor their positions' health ratios or place correctly tuned limits and stop losses to avoid liquidation. This aspect creates stress and complexity for all but the most experienced traders.

### Long Term Leverage

The drawbacks to perps and spot lending make current leverage options unsuitable for **long term investment strategies.** With [$2B open interest](https://coinalyze.net/solana/open-interest/) on SOL and recent auction of billions of dollars worth of locked [SOL from the FTX estate](https://cointelegraph.com/news/ftx-estate-offloads-last-highly-discounted-solana-tokens), there is clear demand for such trades. However, there is currently no leveraged financial instrument on the market which can offer the benefits of increased exposure without the drawbacks that make current approaches impractical and risky.
