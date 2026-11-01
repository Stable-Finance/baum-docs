---
icon: fire
description: Burns of any token on Robinhood Chain, with the data each burner attached.
---

# Burns

Sell something for a burn: a boost, access, a perk. Your app asks people to burn a token and attach a tag, and this endpoint tells you who burned how much and what they attached. Baum reads burns and tags. What a burn buys is up to your app.

## What counts

* **A burn** is a transfer of the token to the zero address (the token's own `burn()`, which lowers total supply) or to the dead address `0x…dead`.
* **A tag** is bytes the burner appended to the end of the call. Tokens ignore extra calldata, so any app can attach a meaning to a burn without a contract. For example, a prefix plus the wallet of the agent being boosted.

A tag can only be read when the burner called the token directly with `burn(uint256)` or `transfer(address,uint256)`. A burn made through another contract shows `data: null`.

## GET /api/burns

Burns of one token, newest first. **A paid call.** See [Credits](../credits.md).

### Query parameters

| Parameter | Required | Meaning |
| --------- | -------- | ------- |
| `token` | Yes | The token's address |
| `tag` | No | Hex, whole bytes, at most 64 bytes. Only burns whose attached data starts with these bytes |
| `wallet` | No | Only this wallet's burns |
| `since` | No | The first block to read. Default `0` |
| `before` | No | Read blocks before this one, to page back. Default: up to the latest block |
| `limit` | No | Rows, 1 to 500. Default `100` |

### Example

```bash
curl "https://baumai.xyz/api/burns?token=0xc17FBa7484bdB276C2b5A7593E14fcAF21155C45&tag=0xabcd1234&limit=50" \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

### Response

```json
{
  "token": "0xc17fba7484bdb276c2b5a7593e14fcaf21155c45",
  "tag": "0xabcd1234",
  "since": 0,
  "to": 1234567,
  "burns": [
    {
      "tx": "0x...",
      "block": 1234500,
      "logIndex": 3,
      "at": 1761990000000,
      "from": "0x...",
      "amount": "1000000000000000000000",
      "via": "burn",
      "data": "0xabcd1234..."
    }
  ],
  "complete": true
}
```

| Field | Meaning |
| ----- | ------- |
| `to` | The last block read |
| `burns[].at` | Block time, in milliseconds |
| `burns[].from` | The wallet whose tokens were burned |
| `burns[].amount` | Raw units, as a string |
| `burns[].via` | `burn` (sent to zero, supply fell) or `dead` (sent to the dead address) |
| `burns[].data` | Everything appended after the call's arguments, as hex. `"0x"` when nothing, `null` when unreadable |
| `complete` | `false` when older matches may exist |

### Paging

When `complete` is `false`, ask again with `before` set to the last row's `block + 1`. Drop rows you've already seen, matching on `tx` and `logIndex`, since one block can hold more than one burn.

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | Which parameter is wrong, for example `token must be a 0x address` or `limit must be 1 to 500` |
| `502` | `chain-unavailable` |

Plus the [common errors](../authentication.md#errors). A non-`2xx` answer is refunded.
