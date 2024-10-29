# Risk Management

### Collateral Ratio

Hylo implements a multi-tiered risk management approach centered around one key metric: the system collateral ratio (CR). The CR is a measure of system health, indicating the ready availability of the backing assets behind hyUSD.

$$
\begin{equation*}
\text{Collateral Ratio} = \frac{\text{TVL} \cdot \text{SOL price}}{\text{hyUSD supply}} \cdot 100%
\end{equation*} \
$$

The system requires a CR over 100% to stably back every dollar worth of hyUSD. When CR is over **150%**, the system is considered fully healthy. If the CR falls to 100% the NAV of xSOL becomes zero and hyUSD loses it hedge, exposing its peg to the full volatility of SOL.

Hylo's risk management system employs two stability mechanisms to keep the CR as high as possible: [**mint/redeem controls**](risk-management.md#id-3.1-stability-mode-1-fee-controls) and the [**stability pool**](risk-management.md#id-3.2-stability-mode-2-stability-pool-drawdown)**.**

### Stability Modes

The protocol may engage two successive stability modes to defend hyUSD's peg, determined by two CR thresholds. The rationale behind these specific thresholds is detailed in the [value-at-risk-analysis.md](../technical-addendum/value-at-risk-analysis.md "mention").

* **Stability Mode 1:** Activated when CR drops **below 150%**
* **Stability Mode 2:** Activated when CR drops **below 130%**

### Stability Mode 1: Fee Controls

When the collateral ratio drops below 150%, the protocol adjusts minting and redemption fees. Fee controls financially incentivize users to perform actions which increase the CR, while disincentivizing actions which decrease it.

* **Decreasing the supply of hyUSD**
  * hyUSD minting fees go up
  * hyUSD redemption fees go down
* **Increasing the supply of xSOL**
  * xSOL minting fees go down
  * xSOL redemption fees go up

#### Fee Table

<table data-header-hidden><thead><tr><th width="229"></th><th width="120"></th><th width="128"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Mode</strong></td><td><strong>hyUSD mint</strong></td><td><strong>hyUSD redeem</strong></td><td><strong>xSOL mint</strong></td><td><strong>xSOL redeem</strong></td></tr><tr><td>Normal</td><td>0.2%</td><td>0.2%</td><td>1%</td><td>1%</td></tr><tr><td>Stability Mode 1</td><td>0.3%</td><td>0.1%</td><td>0.25%</td><td>4%</td></tr><tr><td>Stability Mode 2</td><td>DISABLED</td><td>0%</td><td>0%</td><td>8%</td></tr></tbody></table>

### Stability Mode 2: **Stability Pool Drawdown**

When the collateral ratio crosses the second stability threshold at 130%, signaling severe market volatility, more drastic measures are taken. Fees to control token supplies are more aggressively adjusted and the stability pool is activated.

{% hint style="info" %}
The stability pool provides **steady upward pressure** on the Collateral Ratio (CR) when it falls below 130%. Staked hyUSD in pool is converted to xSOL to support CR recovery.
{% endhint %}

#### Stability Pool Intervention

Introduced in [earning-yield-with-hyusd.md](earning-yield-with-hyusd.md "mention"), the stability pool provides users the opportunity to earn multiplied LST yields from the reserve as a reward for securing the protocol.

When the collateral ratio falls **below 130%**, staked hyUSD in the stability pool is drawn down and converted to xSOL. The double positive effect of **burning hyUSD** and **minting xSOL** quickly recovers the CR a healthy level.

Stability pool users acknowledge this potential swap as a risk, in exchange for financial rewards during normal operation. When users wish to withdraw from the pool during market turbulence, a pro rata share of the minted xSOL is returned to them.



<details>

<summary>Example : Stability Pool usage</summary>

**Starting Scenario: Collateral and Pool Breakdown**

We start with a total of **100 SOL** that backs both hyUSD and xSOL:

* **80 SOL** is backing the stablecoin hyUSD.
* **20 SOL** is backing the leveraged token xSOL.
* The initial **collateral ratio (CR)** is **125%**, meaning 100 SOL backs **80 SOL worth of hyUSD debt** (100 SOL / 80 SOL = 125%).

**Scenario: Redeeming hyUSD into xSOL (Stability Pool)**

Now, let’s assume we redeem **10 SOL worth of hyUSD** into xSOL. This means we reduce the supply of hyUSD while increasing the supply of xSOL. Here’s how the situation changes:

1. **Before Redemption**:
   * **80 SOL** backs hyUSD.
   * **20 SOL** backs xSOL.
   * Collateral ratio = 125% (100 SOL / 80 SOL).
2. **Redemption**:
   * We **redeem 10 SOL worth of hyUSD** into xSOL.
   * After redemption, **70 SOL** will back hyUSD, while **30 SOL** will back xSOL.
3. **After Redemption**:
   * **70 SOL** now backs hyUSD (down from 80 SOL).
   * **30 SOL** backs xSOL (up from 20 SOL).
   * The new **collateral ratio** is: \
     Collateral Ratio = 100 SOL / 70 SOL = **142.5%**

By redeeming **10 SOL** of hyUSD and minting 10 SOL of xSOL, the collateral ratio improves from **125%** to **142.5%**, which is an increase of **17.5%**.

**Why This Works**

* **Leverage and Risk Absorption**: xSOL, being a leveraged token, absorbs more volatility. When hyUSD is redeemed into xSOL, the risk is transferred from the hyUSD to the more volatile xSOL. This allows the collateral ratio to improve efficiently.
* **Efficient Collateral Use**: Redeeming just **10 SOL worth of hyUSD** into xSOL increases the collateral ratio by **17.5%**, showing that xSOL can handle more volatility, thus allowing the system to maintain a higher collateral ratio with minimal SOL redemption.

</details>
