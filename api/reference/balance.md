---
icon: wallet
description: Your key's credit balance and top-up status.
---

# Balance

## GET /api/partner/balance

Your key's credits. **Free.**

### Headers

| Header | Required |
| ------ | -------- |
| `Authorization: Bearer <key>` | Yes |

### Example

```bash
curl https://baumai.xyz/api/partner/balance \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

### Response

```json
{
  "credits": "24987.000123",
  "topUpAmount": 25000,
  "threshold": 6500,
  "lastTopUp": {
    "at": "2026-10-31T14:02:11.000Z",
    "amount": 25000,
    "burnTx": "0x...",
    "treasuryTx": "0x..."
  },
  "lastFailure": null
}
```

| Field | Type | Meaning |
| ----- | ---- | ------- |
| `credits` | string | Credits left, as an exact decimal (1 credit = 1 BAUM) |
| `topUpAmount` | number | BAUM each automatic top-up takes |
| `threshold` | number | The balance below which automatic top-ups start |
| `lastTopUp` | object or null | The last completed top-up, with both transaction hashes on Robinhood Chain |
| `lastFailure` | object or null | The last failed top-up: `at`, `amount` and `reason` |

### Errors

| Status | `reason` |
| ------ | -------- |
| `401` | `no-key`, `bad-key` |
