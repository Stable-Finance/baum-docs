---
description: Five levels — higher reward weight and lower fees as points accrue.
---

# Levels

| Level | Reward weight | Volume fee | API markup | Requirement |
| ----- | ------------- | ---------- | ---------- | ----------- |
| 1     | 1.0×          | 15 bps     | 20%        | Mint |
| 2     | 1.5×          | 12 bps     | 15%        | 1,000,000 pts |
| 3     | 2.0×          | 9 bps      | 10%        | 3,000,000 pts |
| 4     | 3.0×          | 5 bps      | 5%         | 6,500,000 pts + 100,000 BAUM locked |
| 5     | 4.0×          | 2 bps      | 0          | 11,000,000 pts + 250,000 BAUM locked |

Reward weight determines a Broker's share of [sub-DAO allocations](../sub-daos/README.md#token-allocation).

## Locked BAUM

Locked BAUM is **a gate, not an accelerator**: it does nothing below Level 4.

* Levels 4 and 5 hold only while the lock is maintained.
* Unlocking drops the Broker to Level 3 with its points intact.
* Lock requirements halve as BAUM's FDV grows — see [Sunset rule](sunset-rule.md).

Levels travel with the Broker on sale.

## How long it takes

For reference, a Broker lending **$10,000 of USDG** runs at the daily cap and reaches:

| Level | Common Broker |
| ----- | ------------- |
| 2     | \~5 weeks     |
| 3     | \~3 months    |
| 4     | \~7 months    |
| 5     | \~1 year      |

A **Rare** Broker on the same capital reaches Level 5 in about eight months.

$10,000 of LP reaches Level 3 in about ten months.
