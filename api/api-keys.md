---
icon: key
description: How to get a Baum API key, pay for it in BAUM, and manage it.
---

# Getting an API key

You get API keys from Baum itself, in Telegram. There is no sign-up form. Any Baum account can hold one key.

## What you need

* **A Baum account on Telegram.** Message [@BaumReviewBot](https://t.me/BaumReviewBot). See [Baum Agent](../agent/README.md).
* **BAUM in your first EVM wallet with Baum**, plus a little ETH on Robinhood Chain for gas. That wallet pays for the key. If it holds ETH but not enough BAUM, Baum offers to swap for the difference first.
* **A confirmed email.** You can make a key without one, but paid calls are refused with `403 no-email` until your account has a confirmed email. Send `/email you@example.com` to Baum and reply with the 6-digit code it sends. A refused call costs nothing.

## Activate a key

Send this to Baum:

```
/apikey new
```

Baum replies with the terms and a **Confirm** button. Nothing is taken until you confirm.

| | Default | Credits only |
| --- | --- | --- |
| Command | `/apikey new` | `/apikey new 25000` |
| BAUM taken | 35,000 | 25,000 |
| Becomes API credits | 25,000 | 25,000 |
| Goes to your user sponsorship pool | 10,000 | — |

Whatever you pay is split the same way: **80% is burned** with BAUM's own `burn()` and **20% goes to Stable's Safe**. Both transactions are sent from your wallet, and the credits are added only after both confirm. This cannot be undone.

The sponsorship pool pays for Baum credits for the people who come to Baum through your app.

## Save the key

Your key looks like `baum_` followed by 43 characters. Baum sends it to you privately in Telegram. It is never written into your conversation history. Store it somewhere safe, such as your server's secret store.

Anyone with the key can spend your credits. If you lose it, `/apikey show` sends it again. If it leaks, `/apikey rotate` replaces it.

## Automatic top-ups

{% hint style="warning" %}
**Activating a key agrees to automatic top-ups.** When your balance falls below **6,500 credits**, Baum takes **25,000 BAUM** from the same wallet with the same 80/20 split, without asking.
{% endhint %}

* If the wallet can't pay that much, Baum tries **10,000** instead.
* Baum tries once each time the balance falls past a checkpoint: 6,500, 3,900, 2,600, 1,300 and 450 credits, then once more when the balance is too low to pay for a call.
* If a top-up fails, Baum tells you in Telegram. It also emails you when credits are running low, and again when they are almost gone.
* At zero, paid calls answer `402 out-of-credits` until you top up. Your key stays the same.

`/apikey auto <amount>` changes how much each top-up takes. The minimum is 10,000. `/apikey revoke` stops top-ups.

## Commands

| Command | What it does |
| ------- | ------------ |
| `/apikey` | Your credit balance, with **Show key** and **Top up** buttons |
| `/apikey new [amount]` | Activate a key (35,000 by default, at least 25,000) |
| `/apikey show` | Send the key to you again, privately |
| `/apikey topup [amount]` | Top up now (25,000 unless you say) |
| `/apikey auto <amount>` | How much each automatic top-up takes |
| `/apikey pool [amount]` | Add to the pool that sponsors your users' credits (10,000 unless you say) |
| `/apikey rotate` | Replace the key. The old one stops working at once |
| `/apikey revoke` | End the key and its automatic top-ups. Your credits stay on the account |
| `/email <address>` | Link an email. Paid calls need a confirmed one |

You can also check your balance over the API with [`GET /api/partner/balance`](reference/balance.md).
