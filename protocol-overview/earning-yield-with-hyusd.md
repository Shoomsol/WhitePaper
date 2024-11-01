# Earning Yield with hyUSD

hyUSD holders can earn outsized yields while securing the Hylo ecosystem through the Stability Pool. This key earning feature offers users high rewards in exchange for a calculated risk. Technical details about the Stability Pool can be found in [risk-management.md](risk-management.md "mention").

### Yield Generation

When users deposit hyUSD into Hylo's Stability Pool, they receive a Staked hyUSD token representing their pro rata share of the pool. Every epoch, LST yields generated by Hylo's collateral are "harvested" as newly minted hyUSD and automatically compounded into the stability pool. This mechanism causes the Staked hyUSD to continuously appreciate in value.

### Stability Pool APY

Yields for the stability pool are generally a multiple higher than the 7-9% base rate generated by LSTs.

Staked hyUSD holders collect rewards from the entirety of Hylo's TVL, because xSOL and unstaked hyUSD holders do not benefit from the yield on their respective collateral by design. As such, the yields generated by the protocol are shared only among those who stake hyUSD, which is a relatively smaller group. The below chart reflects the "effective yield" on hyUSD compared to what percent of its supply is staked.

<details>

<summary>Example: How the Stability Pool Boosts Yields</summary>

This example demonstrates how the Stability Pool offers significantly higher yields compared to basic SOL staking. However, it's important to note that actual yields may fluctuate based on several key factors, including the amount of hyUSD staked, the total collateral in Hylo, and base LST yield.

1. **Initial Setup**&#x20;

* SOL Reserves: $10 million
* xSOL market cap: $5 million
* hyUSD market cap: $5 million
* Staked hyUSD in Stability Pool: 40%, which equals $2 million
* Base LST Yield: 8% per year, generating $800,000 annually from the $10 million SOL

2. **Reward Distribution**&#x20;

All $800,000 in rewards are given to the $2 million hyUSD staked in the Stability Pool.

* Effective Yield = Total Rewards / Amount Staked
* Calculation: $800,000 / $2,000,000 = 40% yield

Participants in the Stability Pool can earn a 40% yield, five times higher than the base yield of 8%.

</details>

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## Risk Considerations

While the Stability Pool offers attractive earning potential, it also serves a crucial role in Hylo's risk management strategy. Under specific and transparently defined market conditions, deposited hyUSD may be converted to xSOL.

Participants are encouraged to thoroughly review the [risk-management.md](risk-management.md "mention") documentation to gain a comprehensive understanding of the system and its associated risks.
