# Collateral Pool: A Basket of LSTs

Liquid staking tokens (LSTs) are fungible tokens representing staked SOL delegated to one or more validators on the Solana network. LSTs are analogous to an "on-chain bond", where users lend SOL to validators in order to receive "interest" generated from block rewards and MEV. The yield bearing aspect of LSTs makes them an ideal backing collateral for a stablecoin like hyUSD.

* **Initial Composition**: At launch, the pool will accept a limited list of major cap LSTs available on Solana.
* **Future Expansion**: The pool may diversify over time to include new and high performing LSTs, adapting to market developments and opportunities.
* **True Pricing**: Hylo does not rely on an oracle price for any transaction involving LSTs. Instead the true price of each LST is evaluated based on the exact amount of staked SOL in the SPL staking pool program, thanks to an integration with [Sanctum](https://sanctum.so). This means that the Net Asset Value (NAV) calculations for both hyUSD and xSOL are based on the exact SOL price per LST, ensuring consistency and transparency (see [**True LST Value equations**](../technical-addendum/hylo-equations.md#id-1.-true-lst-value)) .

### Collateral Pool Management

Hylo implements fund administration controls which can be utilized by protocol governance to change the makeup and composition of the collateral pool.

* **LST Registry**: The protocol maintains a registry of all LSTs accepted as collateral, and can add new LSTs as the market evolves.
* **Fee Adjustment**: To maintain ideal ratios of each LST in the pool, the protocol employs a dynamic fee system which may discount or increase fees depending on the LST being deposited or withdrawn. This system incentivizes users to help rebalance the pool through normal usage.
