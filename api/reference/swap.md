---
icon: arrow-right-arrow-left
description: Quote buys and sells of tokens launched through Baum, as a transaction the person's own wallet signs.
---

# Swap

Put a swap for any token launched through Baum on your own site. Baum finds where the token trades, prices the trade, and answers with a transaction for the person's own wallet to sign. Baum never holds the funds and never signs for the person.

**Today:** tokens launched through Baum on Robinhood Chain, bought with or sold for the token's pair (ETH). A token still on its Pons bonding curve trades on the curve. A graduated token trades on Uniswap. Baum may add routes later without you changing anything.

## GET /api/partner/swap

Where a token trades and what a wallet holds. **Free.**

### Query parameters

| Parameter | Required | Meaning |
| --------- | -------- | ------- |
| `token` | Yes | The token's contract address |
| `address` | No | A wallet. When given, its balances are included |

### Example

```bash
curl "https://baumai.xyz/api/partner/swap?token=0xc17FBa7484bdB276C2b5A7593E14fcAF21155C45&address=0xYourUserWallet" \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

### Response

```json
{
  "venue": "uniswap",
  "reason": null,
  "pair": { "address": "0x0000000000000000000000000000000000000000", "symbol": "ETH", "decimals": 18, "native": true },
  "decimals": 18,
  "pairBalance": "120000000000000000",
  "tokenBalance": "5000000000000000000000"
}
```

| Field | Meaning |
| ----- | ------- |
| `venue` | `curve`, `uniswap`, or `none` when it can't be traded here right now |
| `reason` | Why not, when `venue` is `none`. Otherwise `null` |
| `pair` | What a buy spends and a sell receives |
| `decimals` | The token's decimals |
| `pairBalance`, `tokenBalance` | The wallet's balances in raw base units, or `null` without `address` |

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | `No token named.` |
| `404` | `Not a token launched through Baum.` |
| `502` | `Couldn't read the market just now.` |

## POST /api/partner/swap

One quote, with the transaction to sign. **A paid call.** See [Credits](../credits.md).

### Body

| Field | Required | Meaning |
| ----- | -------- | ------- |
| `token` | Yes | The token's contract address |
| `side` | Yes | `buy` or `sell` |
| `address` | Yes | The wallet that will sign and send the transaction |
| `amount` | Yes, unless `target` | A string, human-scaled: ETH to spend on a buy, tokens to sell on a sell. `"0.05"` is 0.05 ETH |
| `partnerFee` | No | `{ "recipient": "0x...", "bps": 50 }`. Your own fee on top of Baum's, 0 to 100 basis points (at most 1%) |

A **buy** can also take:

| Field | Meaning |
| ----- | ------- |
| `payWith` | `"ETH"` or the address of a token on Robinhood Chain's list, such as USDG. Defaults to the pair |
| `target` | Tokens to receive, human-scaled, in place of `amount`. Baum works out how much to spend |
| `minOut` | A floor on tokens received, human-scaled, in place of the default slippage floor |
| `totalFeeBps` | A fixed total fee from 100 to 200 basis points, in place of the wallet's usual fee. Your `partnerFee` comes out of it, and Baum keeps the rest. `partnerFee.bps` can't be more than this |

### Fees

* **Baum's fee** is the same as on baumai.xyz, set by the wallet's Deed Deck tier, unless you set `totalFeeBps`.
* **Your partner fee** is taken only where the trade has a Uniswap leg. A plain ETH trade on the bonding curve goes straight to the curve, so there's nowhere to take it. The quote then carries a `partnerFeeNote` saying so. Once the token graduates, the fee is taken.
* The venue's own fee (the curve's fee, or a pool's LP fee) is the market's price and is shown separately as `venueFeePct`.

### Example

```bash
curl -X POST https://baumai.xyz/api/partner/swap \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "token": "0xc17FBa7484bdB276C2b5A7593E14fcAF21155C45",
    "side": "buy",
    "amount": "0.05",
    "address": "0xYourUserWallet",
    "partnerFee": { "recipient": "0xYourFeeWallet", "bps": 50 }
  }'
```

### Response

```json
{
  "venue": "uniswap",
  "side": "buy",
  "fromSymbol": "ETH",
  "toSymbol": "BAUM",
  "fromAmount": "50000000000000000",
  "toAmount": "412345.67",
  "minReceived": "404098.75",
  "feePct": 1,
  "feeAmount": "0.0005",
  "venueFeePct": null,
  "partnerFeePct": 0.5,
  "partnerFeeAmount": "0.00025",
  "impactPct": 0.4,
  "approval": null,
  "transaction": { "to": "0x...", "data": "0x...", "value": "0xb1a2bc2ec50000", "chainId": 4663 }
}
```

| Field | Meaning |
| ----- | ------- |
| `fromAmount` | What is spent, in raw base units |
| `toAmount`, `minReceived` | Expected and minimum received, human-scaled |
| `feePct`, `feeAmount` | Baum's fee, as a percentage and in the input token. Zero on a plain curve trade |
| `venueFeePct` | The curve's fee, or `null` on Uniswap |
| `partnerFeePct`, `partnerFeeAmount` | Your fee, when it could be taken |
| `totalFeePct`, `apiFeePct` | With `totalFeeBps`: the whole fee, and the routing API's part |
| `impactPct` | Price impact, or `null` when unknown |
| `approval` | An allowance the wallet must grant first, or `null`. See below |
| `transaction` | Pass it to the wallet as is: `to`, `data`, `value` (hex) and `chainId` |
| `partnerFeeNote` | Present when you asked for a partner fee that couldn't be taken |

### Approvals

When the wallet spends a token rather than ETH, `approval` names what to approve first:

```json
{ "token": "0x...", "spender": "0x...", "permit2Spender": "0x..." }
```

* On a bonding curve, approve `token` to `spender`. `permit2Spender` is `null`.
* On Uniswap, approve `token` to Permit2 (`spender`), then let `permit2Spender` draw on it through Permit2.

Read the wallet's current allowances before asking for either, so a wallet that already approved isn't asked again.

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | A sentence saying what's wrong: a missing field, an amount the wallet can't cover, a fee out of range, an amount too small |
| `404` | `Not a token launched through Baum.` |
| `409` | Why the token can't be traded here right now |
| `502` | `Couldn't price that trade just now.` or a description of the curve's failure |

Plus the [common errors](../authentication.md#errors). Only a successful quote is charged.
