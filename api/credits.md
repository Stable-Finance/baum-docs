---
icon: coins
description: What the API charges, and when.
---

# Credits and pricing

**1 API credit = 1 BAUM.** You buy credits by [activating or topping up a key](api-keys.md). The BAUM you pay is 80% burned and 20% sent to Stable's Safe.

Most endpoints are free. A few are **paid calls**, and some paper strategy actions have a fixed price in credits.

## What a call costs

A paid call costs **3 credits or $0.001 worth of BAUM, whichever is less.** The price is read from BAUM's market at the time of the call. If no price is available, the call costs 3 credits.

So when BAUM is worth more than $0.000333, a call costs less than 3 credits.

Only a successful call costs anything:

* A refused call costs nothing: no key, a bad key, no confirmed email, or a `400` on the request body.
* If the endpoint answers anything other than `2xx`, the charge is refunded.

Balances are kept to six decimal places, so fractions of a credit are exact.

## Paid endpoints

| Endpoint | Price |
| -------- | ----- |
| `POST /api/partner/swap` (a quote) | One call |
| `GET /api/leaderboard` | One call |
| `GET /api/burns` | One call |
| `POST /api/partner/paper/page` | 100 credits, once per strategy. Asking again for the same strategy is free |
| `GET /api/partner/paper/view` | 10 credits the first time a visitor is seen in an hour, plus 3 when the page is due a refresh. One refresh serves every visitor after it |

Everything else is free, including [`GET /api/partner/swap`](reference/swap.md#get-api-partner-swap) and [`GET /api/partner/balance`](reference/balance.md).

## Your balance

Every response from a one-call endpoint carries your balance after the call:

```
X-Baum-Credits: 24987.000123
```

A `402 out-of-credits` carries it too. You can also check it for free:

```bash
curl https://baumai.xyz/api/partner/balance \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

In Telegram, `/apikey` shows the balance and `/credit` shows your API credits next to your own Baum credits.

## Running out

Automatic top-ups keep a key running. See [Automatic top-ups](api-keys.md#automatic-top-ups). If one can't be paid and your balance reaches zero, paid calls answer `402 out-of-credits` until you send `/apikey topup`. Free endpoints keep working.

{% hint style="info" %}
API credits are separate from the Baum credits you spend chatting with [Baum Agent](../agent/credits-and-invites.md).
{% endhint %}
