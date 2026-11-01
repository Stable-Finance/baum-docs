---
icon: copy
description: Read and change a signed-in person's copy agents and the limits they copy with.
---

# Copy agents

A copy agent buys and sells when the wallets it copies do, inside limits its owner sets. See [Copy trading and copy agents](../../agent/what-it-can-do.md#copy-trading-and-copy-agents).

These endpoints read and change the same settings as **Edit** under a copy agent in Baum. Both are **free**, and both need a session:

```
Authorization: Bearer <key>
X-Baum-Session: <session>
```

{% hint style="info" %}
**Changing values doesn't start or stop anything.** A running agent keeps running on the new values. A new copy agent still needs its owner to tap **Confirm** in Baum before it trades.
{% endhint %}

## GET /api/partner/copy

Their defaults, each copy agent and each copy in it with its values, and each value's bounds.

```bash
curl https://baumai.xyz/api/partner/copy \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

```json
{
  "defaults": { "sizeUsd": 25, "perTradeUsd": 300, "dailyUsd": 10000, "maxImpactPct": 5, "pauseAtLossPct": 30, "skipInsiderTokens": true },
  "agents": [
    {
      "id": "main",
      "name": "main",
      "status": "active",
      "address": "0x...",
      "copies": [
        {
          "ref": "agent:0x...",
          "label": "frank-oak",
          "url": "https://...",
          "sizing": "$25 per buy",
          "values": { "sizeUsd": 25, "perTradeUsd": 300, "dailyUsd": 10000, "maxImpactPct": 5, "pauseAtLossPct": 30, "skipInsiderTokens": true },
          "custom": false,
          "pending": false
        }
      ]
    }
  ],
  "fields": [
    { "key": "sizeUsd", "label": "Amount per buy", "min": 1, "max": 10000, "unit": "usd" }
  ]
}
```

| Field | Meaning |
| ----- | ------- |
| `agents[].status` | `draft` (never confirmed), `active` or `paused` |
| `agents[].address` | The wallet it trades from. `null` until its first Confirm |
| `copies[].custom` | `true` when this copy has its own limits, `false` when it uses the defaults |
| `copies[].pending` | Added to a running agent and waiting for Confirm |
| `fields` | Every value's label, bounds and unit (`usd`, `pct` or `toggle`), for building a form |

The values shown above are an example. Read the real ones from `defaults`, and the bounds from `fields`.

## POST /api/partner/copy

New values, applied to what the person chose.

### Body

| Field | Meaning |
| ----- | ------- |
| `values` | Any of `sizeUsd`, `perTradeUsd`, `dailyUsd`, `maxImpactPct`, `pauseAtLossPct`, `skipInsiderTokens` |
| `apply` | What the new values apply to. See below |

| `apply` | Changes |
| ------- | ------- |
| `"future"` | The defaults, for copies set up from now on |
| `"all"` | The defaults and every copy |
| `{ "copies": [{ "agent": "<id>", "ref": "<ref>" }] }` | The defaults and these copies. The rest keep their values |
| `{ "copy": { "agent": "<id>", "ref": "<ref>" } }` | That one copy only. The defaults stay |

| Value | Meaning |
| ----- | ------- |
| `sizeUsd` | Dollars per buy |
| `perTradeUsd` | The most on one buy |
| `dailyUsd` | The most a day |
| `maxImpactPct` | The highest price impact a copied trade may take |
| `pauseAtLossPct` | Pause copying at this loss |
| `skipInsiderTokens` | Skip tokens with heavy insider holdings |

### Example

```bash
curl -X POST https://baumai.xyz/api/partner/copy \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..." \
  -H "Content-Type: application/json" \
  -d '{"values":{"dailyUsd":250,"maxImpactPct":3},"apply":"all"}'
```

Answers the settings after the change, in the same shape as `GET`.

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | `Send values to change.`, a sentence about `apply`, or which value is out of bounds |
| `401` | `signed-out` |

Plus the [common errors](../authentication.md#errors).
