---
description: Where a Broker goes to work.
---

# Portal overview

{% hint style="info" %}
**Baum is in private beta.** Beta opens to all Deed Deck holders around October 1.
{% endhint %}

The Portal is where a Broker goes to work. The owner:

1. funds the Broker's wallet with **USDX, USDG, or ETH**,
2. selects the [actions](actions.md) Baum should take, and
3. a Baum instance tied to that wallet executes them.

## Scoped authorization

Baum operates under a scoped authorization on the wallet:

* **Allowlisted contracts only** — core pools, the lending market, the vault, locks, governance.
* **Maximum slippage.**
* **No outbound transfers** except to the Broker's owner.

The owner retains custody through the NFT.

Instances sleep at zero balance and wake on deposit.
