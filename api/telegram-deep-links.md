---
icon: paper-plane
description: Links that open Baum in Telegram ready to launch, copy, sign in or trade, with your referral code.
---

# Telegram deep links

A deep link opens a chat with Baum and tells it why the person came. Every link is a Telegram start parameter on Baum's bot:

```
https://t.me/BaumReviewBot?start=<parameter>
```

Each link carries your referral code. When someone who is new to Baum arrives on your link, the referral is recorded to you. An account keeps the first referral it gets. Baum on Telegram is invite only, and a valid referral code is one way in.

Find your code with `/referral` in Baum. Codes are upper case letters, digits and dashes.

## Links

| Parameter | What Baum does |
| --------- | -------------- |
| `ref-CODE` | Records the referral and says hello |
| `atp-launch-CODE` | Offers to launch a new [trading agent](../agent/what-it-can-do.md#trading-agents), and walks the person through it |
| `atp-copy-<address>-CODE` | Sets up a [copy agent](../agent/what-it-can-do.md#copy-trading-and-copy-agents) for that wallet and shows it with **Confirm** |
| `atp-login-CODE` | Sends a one-time link that signs the person in to your site. See [Sign in with Baum](sign-in-with-baum.md) |
| `atp-register-CODE` | Explains how to bring an agent to Baum today (listing an agent that runs outside Baum isn't supported yet) |
| `trade-0x<address>` | Opens Baum on one Robinhood Chain token, ready to trade it |
| `tr-<address>-CODE` | The same, with your referral code |

Prefixes are case-insensitive, and Baum reads codes in upper case.

## Examples

```
https://t.me/BaumReviewBot?start=ref-ABCD-1234
https://t.me/BaumReviewBot?start=atp-launch-ABCD-1234
https://t.me/BaumReviewBot?start=atp-copy-5b38da6a701c568545dcfcb03fcb875f56beddc4-ABCD-1234
https://t.me/BaumReviewBot?start=atp-login-ABCD-1234
https://t.me/BaumReviewBot?start=tr-c17fba7484bdb276c2b5a7593e14fcaf21155c45-ABCD-1234
```

## Rules

* **64 characters at most.** That is Telegram's limit for the whole parameter. A link over it doesn't work.
* **Addresses go without `0x`** in `atp-copy-` and `tr-` links, to leave room for the code. An address with `0x` still works if it fits. `atp-copy-` plus an address is 50 characters, which leaves 13 for the code.
* **A missing or malformed code drops the referral, not the link.** The person still gets what the link was for.
* **Copying still needs Confirm.** An `atp-copy-` link sets up the copy at the default amount and limits, and the person checks them and taps **Confirm** before anything trades.
