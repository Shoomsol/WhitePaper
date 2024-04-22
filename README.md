# Lite Paper

Hylo introduces an innovative framework for a decentralized stablecoin on Solana, designed for scalability and improved performance. Building upon the foundational concepts borrowed from the [f(x) protocol](https://fx.aladdin.club/) on Ethereum, Hylo has refined and adapted these ideas to enhance functionality and increase stability of the system by expanding it to be monolithic, support multiple liquid staked tokens (LST) and change the stability modes escalations. It features two SOL-based derivatives: hyUSD, a stablecoin designed to maintain a 1:1 peg with the USD, and levSOL, a token representing a leveraged position on SOL.&#x20;

## 1. hyUSD, a decentralized stablecoin

hyUSD is designed to consistently match the value of the US dollar on a 1:1 basis, achieved by overcollateralizing it with liquid staked SOL. This system allows for the minting of hyUSD by depositing an equivalent value of SOL—every $1 worth of SOL deposited enables the minting of one hyUSD. Similarly, SOL can be redeemed using hyUSD at any moment, ensuring a seamless and continuous exchange mechanism.

## 2. The levSOL

levSOL is a token representing a leveraged long position on SOL, with variable leverage and an extremely low probability of liquidation. It replicates and intensifies the spot price movements of SOL, with algorithmic adjustments made in response to fluctuations in SOL's price. levSOL can be minted by providing SOL equivalent to its current value (Describe in section 3.), and conversely, it can be burned to redeem SOL.

The main advantage of levSOL, compared to other methods to leverage investors exposure to SOL, is that it offers this leverage free from funding rates.

## 3. Symbiotic relationship between levSOL and hyUSD

levSOL and hyUSD share a symbiotic relationship, where levSOL acts as a buffer, absorbing SOL's volatility. This arrangement facilitates the stability of hyUSD, enabling it to maintain its 1:1 peg with the USD despite market fluctuations. This interdependence not only enhances the robustness of hyUSD but also leverages the inherent volatility of SOL to the advantage of levSOL holders.&#x20;

### 3.1. Algorithm adjustment

The price of levSOL is dynamically adjusted depending on the price of SOL, ensuring that the market capitalisation of hyUSD  plus the market capitalisation of levSOL supply always equals the SOL reserve's value. This mechanism allows both hyUSD and levSOL to be redeemed at their Net Asset Value (NAV) at any time, based on the following equation:



$$
n_{sol} * p_{sol} = n_{hyusd} * p_{hyusd} + n_{levsol} * p_{levsol}
$$

Where:

* $$n_{sol}$$ = Amount of SOL in the reserve
* $$p_{sol}$$ = Spot price of SOL
* $$n_{hyusd}$$  = Current supply of hyUSD
* $$p_{hyusd}$$  = Current price of hyUSD, pegged at 1
* $$n_{levsol}$$  = Current supply of levSOL
* $$p_{levsol}$$  = Current price of levSOL

The protocol dynamically adjusts levSOL's price to maintain this balance.

{% hint style="info" %}
For example, if the SOL price is $100 and there's 1 SOL in reserve with a supply of 50 hyUSD and 50 levSOL, both the hyUSD and levSOL market caps would be $50, setting the levSOL price at $1. If SOL's price increases to $200, the reserve value would be $200, but with only still 50 hyUSD backed by this reserve, levSOL's price would adjust to reflect a new market cap of $150, resulting in a levSOL price of $3, to balance the equation.
{% endhint %}

### 3.2. Stability mode

To enhance the stability of the protocol and ensure that hyUSD consistently maintains its peg, the protocol incorporates a backstop mechanism to respond effectively in the event of a market high volatility, aimed at restoring the protocol to a healthy collateralization ratio.

The collateralization ratio of hyUSD is determined at any given moment by dividing the market capitalization of hyUSD by the current value of the SOL reserves. This metric serves as a crucial indicator of the protocol's health and its ability to maintain the peg of hyUSD against US dollar. To safeguard protocol stability and the integrity of hyUSD value, the system is designed to activate one or two stability modes depending on the current collateralization ratio:

**Normal Mode:** This mode operates when the collateralization ratio is above 150%, indicating that the protocol is in a stable condition. During this mode, the protocol functions under regular operations with standard minting and burning fees for hyUSD and levSOL, as well as typical operations of stability pools.

**Stability Mode 1:** Activated when the collateralization ratio drops below 150%, signaling potential market instability or stress. In this mode, specific measures are implemented to encourage users to burn hyUSD and mint levSOL.

**Stability Mode 2:** Initiated when the collateralization ratio decreases below 130%, highlighting more severe market instability or stress. This mode directly engages in burning hyUSD and minting levSOL using the stability pool to restore the collateralization ratio to above 130%.

The protocol's ability to switch between these modes ensures a flexible and responsive strategy to maintain stability. This dynamic approach allows the protocol to adapt to market conditions, thereby protecting users' investments and maintaining the reliability of hyUSD peg to its underlying assets.

#### 3.2.1. Stability Mode 1, minting and burning control

The protocol employs a method to adjust its collateral ratio above 150%, aiming to maintain a healthy level, through the control of minting and burning processes for hyUSD and levSOL. Specifically, by decreasing the supply of hyUSD, the collateral ratio is increased. Conversely, by augmenting the supply of levSOL, the collateral ratio also rises. In contrast, increasing the supply of hyUSD or decreasing the supply of levSOL would have the opposite effect, lowering the collateral ratio.

When the protocol's collateral ratio drops below 150%, certain measures are taken concerning minting and burning fees, as detailed below:

<table data-header-hidden><thead><tr><th width="229"></th><th width="120"></th><th width="128"></th><th></th><th></th></tr></thead><tbody><tr><td>Mode</td><td>hyUSD mint</td><td>hyUSD burn</td><td>levSOL mint</td><td>levSOL burn</td></tr><tr><td>Normal (Collateral Ratio > 150%)</td><td>0.25%</td><td>0.25%</td><td>1%</td><td>1%</td></tr><tr><td>Stability Mode 1 (Collateral Ratio &#x3C; 150%)</td><td>N/A (disable)</td><td>0%</td><td>0%</td><td>8%</td></tr></tbody></table>

In **Stability Mode 1**, the protocol disables the minting of hyUSD, and fees for burning hyUSD are eliminated. Additionally, this mode allows for the minting of levSOL without incurring any fees, while significantly increasing the cost associated with burning levSOL.

This approach is designed to naturally encourage the burning of hyUSD and the minting of levSOL, thereby helping to restore the collateral ratio to a healthy level.

#### 3.2.2. Stability mod 2, Stability pool usage

Users can deposit their hyUSD into a stability pool at any time to earn a portion of the yield generated by the liquid staked SOL from the reserve. If the protocol's collateralization ratio ever falls below 130%, the stability pool will be utilized to restore the ratio to above 130%.

There are two types of stability pools:

* hyUSD - SOL Stability Pool: Deposits made in this pool are used to burn hyUSD in exchange for redeeming SOL from the protocol until the collateralization ratio is above 130%. Burning hyUSD effectively reduces the collateralization ratio because it decreases the amount of hyUSD backed by the reserve.
* hyUSD - levSOL Stability Pool: This pool operates in a manner similar to the hyUSD - SOL stability pool. Whenever the collateralization ratio falls below 130%, hyUSD is converted into SOL, and this SOL is then converted into levSOL. This process actively burns hyUSD while minting levSOL, reducing the amount of hyUSD to be backed by the reserve and simultaneously increasing the amount of SOL backing the hyUSD.

Minting premiums will also be awarded in HYLO tokens to further incentivize users to mint levSOL.

These mechanisms ensure that the protocol maintains a healthy collateralization ratio, thereby enhancing stability and security for all participants.&#x20;

## 4. Economic model of Hylo

Hylo is designed to generate revenue through two main channels. The initial source of income comes from the fees incurred during the minting and burning processes (detailed in [section 3](./#id-3.2.1.-stability-mode-1-minting-and-burning-control)). However, the majority of Hylo's revenue is expected to be derived from the yield produced by staked SOL. The SOL held in the reserve is projected to yield an Annual Percentage Yield (APY) of around 7-8%. A portion of this yield will be allocated to those participating in the stability pools, with the remaining yield serving as a direct source of revenue for Hylo.&#x20;

## 5. The HYLO token

The HYLO token serves as the cornerstone of governance within the Hylo ecosystem, empowering holders with the authority to influence future decisions and directions of the protocol. Beyond its pivotal role in governance, HYLO also enhances the Hylo framework by offering additional incentives and benefits to its users:

1. **Governance**: HYLO token holders are granted voting rights, allowing them to participate in key decisions that shape the protocol's development, policy updates, and operational adjustments. This ensures that the Hylo community has a direct impact on the platform's evolution and governance.
2. **Stability Pool Rewards**: To bolster the attractiveness and effectiveness of the stability pools, HYLO tokens might be distributed as rewards. This strategy not only enhances the yield for participants who contribute to the stability of the system by depositing assets into these pools but also strengthens the protocol's overall health and resilience.
3. **Premium Rewards for Minting levSOL**: In scenarios where the collateralization ratio dips below 130%, signifying heightened market stress, HYLO tokens are awarded as premiums to users who mint levSOL. This mechanism serves a dual purpose: incentivizing the minting of levSOL to aid in restoring the collateralization ratio and rewarding users for participating in activities that contribute to the protocol's stability during critical periods.

Through these utilities, the HYLO token is designed to foster a robust, participatory governance model, increase the protocol's stability, and reward users for their contributions to the ecosystem's health and growth.

## 5. Conclusion

In summary, Hylo introduces to Solana a novel approach to decentralized stablecoins, creating a scalable and stable ecosystem with hyUSD and levSOL. This innovative framework not only ensures that hyUSD maintains its peg to the USD but also allows for potential growth through leveraged positions on SOL via levSOL. Furthermore, Hylo offers an attractive proposition for investors seeking Solana staking yields without direct exposure to SOL price movements, by enabling the staking of hyUSD into the stability pools. Coupled with Stability Modes and the strategic application of the HYLO governance token, Hylo presents a comprehensive system for sustaining protocol stability and fostering community involvement.

\
\


\
\




\
