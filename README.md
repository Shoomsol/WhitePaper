---
description: 🚧 Confidential work in progress - please do not share outside. 🚧
cover: .gitbook/assets/HYLO-Lite.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Hylo Litepaper

### Abstract

Hylo introduces an innovative framework for a decentralized stablecoin on Solana. Designed for scalability and interoperability, the Hylo protocol consists of two SOL-backed derivative tokens: **hyUSD**, a stablecoin designed to maintain a 1:1 peg with the US dollar and **xSOL**, a leveraged long position on SOL.

Hylo takes inspiration from foundational concepts first published by the [f(x) protocol](https://docs.aladdin.club/f-x-protocol) on Ethereum, further refining the approach for the Solana ecosystem. The user experience on Hylo is simplified by pegging the value of hyUSD to exactly $1 worth of SOL, while allowing the volatility of the underlying assets to be absorbed by the xSOL token's price. Further, Hylo admits a diverse basket of Solana liquid staking tokens (LSTs) as yield-bearing collateral and hardens security with financially incentivized stability mechanisms.

### Overview

#### hyUSD, a decentralized stablecoin

hyUSD is designed to consistently match the value of the US dollar on a 1:1 basis, achieved by over-collateralizing it with liquid staked SOL. When hyUSD is minted, an equivalent value of an LST is deposited into the collateral pool. At any time, hyUSD tokens can be redeemed for any of the deposited LSTs, creating a seamless and continuous exchange with high liquidity.

#### xSOL, a leveraged long without liquidation risk

xSOL is a token representing a long position on SOL, replicating and intensifying its spot price movements through a simple pricing formula. xSOL can be minted by depositing an amount of LST equivalent to its current net asset value (NAV) and can later be redeemed at a higher or lower multiple depending on direction of the market, not unlike a perpetual future.

The leverage behind xSOL depends on the market's fluctuation: the effective leverage increases as SOL goes down, and reflexively decreases when SOL goes up. The main advantages of xSOL compared to perpetual futures are that it offers this leverage free from funding rates and liquidation risk. Investors are only charged a flat fee to enter or exit their positions, and instead of facing liquidation during extreme market turbulence, they are exposed to the xSOL price approaching zero.

#### Symbiotic relationship between hyUSD and xSOL

The name Hylo is derived from Aristotle's [hylomorphism](https://en.wikipedia.org/wiki/Hylomorphism), a philosophical notion that all natural things are comprised of matter (the body) and form (the soul). True to this concept, xSOL and hyUSD share a symbiotic relationship to form the whole of the collateral pool behind Hylo. Where the fixed body of hyUSD is a safe store of value, xSOL acts as a dynamic buffer absorbing SOL's volatility to balance the equation. This arrangement facilitates the stability of hyUSD's peg despite market fluctuations, while simultaneously enabling xSOL holders to take outsized returns from the same.

#### Stability Pool

Beyond the core tokens, Hylo provides users the opportunity to stake hyUSD in a stability pool to secure the protocol. The stability pool operates similarly to a lending or market making fund, where the risk of drawdown is traded off for magnified yields from the LST vaults, a share of fees, and other configurable rewards including the [$HYLO governance token](./#hylo-governance-token). As its name implies, the pool is utilized in one of the protocol's stability modes where it may convert some amount of the staked hyUSD to xSOL to re-stabilize the stablecoin peg.

### Protocol Mechanics

#### The Hylo Equation

The total value locked (TVL) in Hylo's vaults must always be equivalent to the sum of the market capitalizations of the hyUSD and xSOL tokens.

$$
\begin{equation*}
n_{sol} \cdot p_{sol} = n_{hy} \cdot p_{hy} + n_{x} \cdot p_{x}
\end{equation*} \\

where \space \space \space

\begin{align*}
  \\ n_{sol} & = \text{SOL in reserve}
  \\ p_{sol} & = \text{SOL spot price}
  \\ n_{hy} & = \text{hyUSD supply}
  \\ p_{hy} & = \text{hyUSD NAV, always \$1}
  \\ n_{x} & = \text{xSOL supply}
  \\ p_{x} & = \text{xSOL NAV}
\end{align*}
$$

It is worthwhile to note that the expression $$n_{sol}$$ is a shorthand equivalent to the sum of all SOL backed by the LSTs stored in Hylo's vaults. For each LST, the price of that token in terms of SOL is computed on chain through the balance in its respective staking pool.

$$
n_{sol} = \sum_{\text{lst} \in \text{vault}} n_{lst} \cdot p_{lst}
$$

#### Pricing hyUSD and xSOL

The price of the hyUSD token is always fixed to one US dollar, so we can effectively drop $$p_{hy}$$ from subsequent formulas. The Hylo equation can then be rearranged to determine how the protocol dynamically adjusts xSOL's price.

$$
p_x = \frac {n_{sol} \cdot p_{sol} - n_{hy}} {n_x}
$$

We can observe that the price of xSOL depends on the amount of unreserved collateral in the system divided by its token supply. As the amount of unreserved collateral grows, implying a price appreciation in SOL, the price of xSOL increases. Likewise if the SOL price dips, the price of xSOL decreases to entice investors into opening leveraged positions to balance the protocol.

{% hint style="info" %}
Let's say the SOL price is $100, there is 1 SOL deposited in the pool, and there is a supply of 50 hyUSD and 50 xSOL floating. With a value of $100 in the pool and $50 worth of reserved collateral for hyUSD, the price of xSOL is $50 / 50 or $1.\
\
If SOL's price subsequently increases to $200, the reserve value becomes $200. Without minting any new tokens, there are still only $50 worth of hyUSD to guarantee with the reserve. Thus the market cap of xSOL increases to $150 and results in the price jumping to $3.\
\
Conversely, if the price of SOL drops to $75 this leaves only $25 of unreserved collateral left for xSOL and negatively impacts its price to $0.50.
{% endhint %}

#### Effective Leverage of xSOL

At any given time, the effective leverage on xSOL is computed by the ratio of the total value locked to its market cap. The leverage increases with the amount of hyUSD minted in system, which adds collateral under management but does not change the supply of xSOL. Leverage related risks are managed by Hylo's stability mechanisms, described in the subsequent sections, which aim to incentivize minting of xSOL and burning of hyUSD.

$$
L_x = \frac {n_{sol} \cdot p_{sol}} {n_x \cdot p_x}
$$

### Stability Modes

#### Collateral Ratio

The most important operating metric in Hylo is the collateral ratio (CR), which compares the protocol's available SOL collateral against the floating market cap of hyUSD. This ratio is ultimately a measure of the protocol's health and liquidity, and it must stay above 100% to maintain hyUSD's peg.

$$
CR = \frac {n_{sol} \cdot p_{sol}} {n_{hy}} \cdot 100\%
$$

Hylo incorporates two layers of stability controls intended to respond to high volatility events in the market. The primary goal of these mechanisms is to keep the collateral ratio as high above 100% as possible. Each stability mode is triggered by the collateral ratio crossing one of the two configured stability thresholds. The protocol is able to dynamically switch between stability modes in response to market conditions, protecting users' investments and maintaining hyUSD's peg to the underlying LSTs.

#### Normal Mode

When the collateral ratio is above 150%, the protocol is considered to be fully stable and healthy. During this normal mode, the protocol admits all regular operations with standard minting and redemption fees for hyUSD and xSOL.

#### **Stability Mode 1: Fee Controls**

If the collateral ratio drops below 150% the first stability mode is engaged, signaling downward pressure on the price of SOL or increased demand for hyUSD. In this first mode, financial incentives are activated in the protocol's fees to encourage users act on behalf of its health.

We know from its [definition](./#collateral-ratio) that the collateral ratio may be increased by either burning hyUSD or augmenting the supply of xSOL. To promote these activities in the first stability mode, mint fees for hyUSD are increased while redeem fees are decreased. On the other hand, xSOL mint fees are decreased while redeem fees are increased. The below table compares the fees between the normal and stability modes.

<table data-header-hidden><thead><tr><th width="229"></th><th width="120"></th><th width="128"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Mode</strong></td><td><strong>hyUSD mint</strong></td><td><strong>hyUSD redeem</strong></td><td><strong>xSOL mint</strong></td><td><strong>xSOL redeem</strong></td></tr><tr><td>Normal</td><td>0.5%</td><td>0.5%</td><td>1%</td><td>1%</td></tr><tr><td>Stability Mode 1</td><td>0.75%</td><td>0.25%</td><td>0.5%</td><td>2%</td></tr><tr><td>Stability Mode 2</td><td>DISABLED</td><td>0%</td><td>0%</td><td>8%</td></tr></tbody></table>

#### **Stability Mode 2: Stability Pool Drawdown**

If the collateral ratio crosses the second stability threshold at 130%, this highlights severe market instability or stress. In this second mode, the minting of hyUSD is entirely disabled and its redeem fees are dropped to zero. Additionally, xSOL's mint fees are taken to zero while redeem fees are escalated to an unpalatable number.

Beyond the drastic changes to fees, stability mode two directly engages in drawing down hyUSD from the [stability pool](./#stability-pool) and minting xSOL in its place to recover the collateral ratio above 130%. The potential for this swap is acknowledged by stability pool users as a risk in exchange for financial rewards in normal operation, and the minted xSOL is made available to users when they withdraw from the pool.

### Economic Model

Hylo is designed to generate revenue through two main channels. The initial source of income comes from the fees incurred during the minting and burning processes. However, the majority of Hylo's revenue is expected to be derived from the yield produced by its LST vaults. A significant portion of this yield will be allocated to users participating in the stability pool, with the remaining yield serving as a direct source of revenue for the treasury.

LSTs are the lifeblood of Hylo, and the protocol intends to accept most yield-bearing LSTs with a significant market capitalization. In order to maintain a healthy balance of LSTs in the vaults, protocol governance may implement fee incentives for tokens it intends to overweight. A diversity in the backing collateral will mitigate the risks related to specific LSTs de-pegging or otherwise losing value.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Source: <a href="https://dune.com/0xplish/solana-lst-market">https://dune.com/0xplish/solana-lst-market</a></p></figcaption></figure>

### $HYLO Governance Token

The $HYLO token serves as the cornerstone of governance for the protocol. Token holders are granted voting rights, allowing them to participate in key decisions that shape the protocol's development, policy updates, and operational adjustments.

$HYLO may be rewarded to users for their participation in the protocol:

1. **Stability Pool Rewards**: To bolster the attractiveness of stability pools, $HYLO tokens may be distributed as rewards to stakers.
2. **Premium Rewards for Minting xSOL**: In stability mode 2, $HYLO tokens may be awarded as premiums to users who mint xSOL. This mechanism serves a dual purpose in restoring the collateral ratio and rewarding users for participating in activities that contribute to the protocol's stability during critical periods.
3. **Staking with featured LSTs:** Users can be rewarded with $HYLO for staking their SOL with specific LSTs the protocol may be partnered with or directly operating.

Through these utilities, the HYLO token is designed to foster a robust and participatory governance model, increase the protocol's stability, and reward users for their contributions to the ecosystem's health and growth.

### Conclusion

In summary, Hylo introduces to Solana a novel approach to the decentralized stablecoin, creating a scalable and stable financial layer for the on-chain economy. The protocol offers an attractive proposition for investors seeking leveraged long exposure with xSOL, or Solana staking yields without direct exposure to SOL price movements through its hyUSD stability pool. Over time, Hylo will ideally become a community governed effort with community engagement, a rich partner network, and integrations into core financial systems on Solana.
