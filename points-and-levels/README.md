---
description: How a Broker's wallet earns points.
---

# Earning points

Points are earned by a Broker's wallet, computed several times per day, and published as a snapshot hash whenever an allocation is paid so holders can verify their share.

## Rates

| Action                        | Rate                   |
| ----------------------------- | ---------------------- |
| USDG lent to the USDX market  | 3 pts per $1 per day   |
| LP in a core pool             | 1 pt per $1 per day    |
| USDX held                     | 1 pt per $10 per day   |
| mUSDX held                    | 1 pt per $25 per day   |
| USDX/USDG swap volume         | 1 pt per $100          |
| BAUM and sub-DAO pair volume  | 1 pt per $60           |
| Governance vote cast          | 1,000 pts              |
| **Daily cap, per Broker**     | **30,000 pts**         |

## Daily cap

The daily cap is what shapes the ladder. It is reached by any of:

* $10,000 of USDG lent
* $30,000 of LP
* $300,000 of USDX held

Capital beyond that earns nothing more on a single Broker; **the way to earn more is more Brokers.**

The [Multiplier Attribute](../brokers/traits.md#multiplier-attribute) is applied after the cap:

| Multiplier | Max points per day |
| ---------- | ------------------ |
| Common     | 30,000             |
| Uncommon   | 37,500             |
| Rare       | 45,000             |

## Rules

* Swap points are counted **net of fees paid**.
* Governance points are awarded only for votes on proposals that reach the backing threshold (see [Governance](../sub-daos/governance-and-revenue.md#governance)).
* Points **decay approximately 3% per week** when a Broker is idle.
