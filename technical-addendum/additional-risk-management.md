# Additional Risk Management

## Minting and Redeeming Bounty

In most situations where the collateral ratio falls below 130%, the steady and continuous upward pressure from the Rebalancing Pool will quickly restore it, maintaining system stability. Issues only occur if the downward pressure on the CR is sustained or severe enough to exhaust the stability pool's supply of hyUSD.&#x20;

To speed up and support the CR's recovery while reducing reliance on rebalancing pool funds, a special reserve of accumulated treasury revenue is available to provide **bonuses** to users who **mint xSOL or redeem hyUSD** in Stability Mode. These bonuses offer users (or bots) an immediate arbitrage opportunity to buy and redeem hyUSD from external liquidity pools.&#x20;

Moreover, the combination of a **minting bonus and high xSOL leverage** under these conditions makes xSOL minting highly appealing. Minting xSOL has an even more significant positive impact on system stability than hyUSD redemptions, and the combination of both provides a robust backstop in any market condition.

The combination of the Stability Pool and these bounty mechanisms creates a strong defense against severe price drops, offering multiple layers of protection to ensure the protocol's stability.

### Recapitalization

In the most extreme scenarios, where insufficient hyUSD is available to stabilize the protocol and the probability of destabilization becomes unacceptably high, Hylo has the ability to implement a recapitalization process. This process utilizes the accumulated treasury funds to recapitalize the protocol.

* Minting xSOL: Using the accumulated SOL to mint xSOL, directly increasing the collateralization ratio.
* Buying and Redeeming hyUSD: Purchasing hyUSD from the market and redeeming it, reducing the supply of hyUSD and improving the CR.

This recapitalization mechanism serves as a last resort to ensure the protocol's stability in extreme market conditions, providing an additional layer of security for users and stakeholders.

### Additional Metrics

In addition to the CR, Hylo utilizes two additional metrics to provide a more comprehensive view of the system's health:

* **Stability Pool Adjusted Collateral Ratio**: This represents the collateral ratio if the entire stability pool's hyUSD were converted into xSOL. It provides insight into the system's resilience considering its built-in stability mechanism.
* **The Buyback Adjusted Collateral Ratio at 1% Premium**: This metric shows the collateral ratio if all hyUSD available on decentralized exchanges (DEX) at a maximum 1% premium ($1.01 per hyUSD) were bought back and redeemed for SOL. It offers a view of the system's health considering immediate market liquidity.

The Adjusted Collateral Ratio, which considers both the stability pool and available liquidity for buyback, is a key metric in Hylo's risk management strategy. It provides a more conservative and comprehensive view of the system's health compared to the System CR alone.
