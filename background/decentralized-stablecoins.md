# Decentralized Stablecoins

### The Stablecoin Trilemma <a href="#the-stablecoin-trilemma" id="the-stablecoin-trilemma"></a>

The Stablecoin Trilemma posits that a stablecoin implementation can only achieve two of three properties: **decentralization**, **price stability**, and **capital efficiency**.

Centralized stablecoins like USDC and USDT solve for **capital efficiency** and **price stability**, maintaining a 1:1 backing ratio while mostly avoiding depegging.

Decentralized stablecoins have gained prevalence since 2021. These alternative assets are not exempt from the trilemma and face unique challenges due to the hedging strategies used to mitigate volatile cryptocurrency collateral.&#x20;

<div data-full-width="false">

<figure><img src="../.gitbook/assets/Stablecoin Trilemma.png" alt="" width="563"><figcaption></figcaption></figure>

</div>

### Decentralized Stablecoin Strategies

#### Collateral Debt Position (CDP)

Popularized by MakerDAO's DAI, the core mechanic in CDP stablecoins is debt. The user borrows the stablecoin by depositing digital assets in a 1.5:1 or 2:1 ratio. This over-collateralization hedges the volatility of the digital asset for price **stability** while sacrificing **capital efficiency**. As such, CDPs have struggled with scalability as their growth is tightly linked to on-chain borrowing demand.

#### Algorithmic Stablecoins

The most well-known algorithmic stablecoin in recent history was [UST](https://www.coindesk.com/learn/the-fall-of-terra-a-timeline-of-the-meteoric-rise-and-crash-of-ust-and-luna/) by Terra Labs. UST's peg was not tied to a collateral asset but rather the minting and burning of LUNA, Terra blockchain's native currency. In May 2022, a financial attack on LUNA triggered a bank run on UST, vaporizing billions in user funds. Since UST's collapse, algorithmic stablecoins have been avoided due to their inherently vulnerable tokenomics.

#### Delta-Neutral Synthetic Dollars

Delta-neutral synthetic dollars like Ethena's USDe are financially engineered with a [cash and carry](https://www.investopedia.com/terms/c/cashandcarry.asp) trading strategy. Collateral assets are accepted 1:1 to mint the synthetic dollar, while a trading system in the issuer's backend manages short positions against the same asset. In the event of downward price movement, the shorts becomes profitable to mitigate losses incurred by the collateral pool. While capital efficient and stable, synthetic dollars slip with decentralization due to their dependence on centralized exchanges.
