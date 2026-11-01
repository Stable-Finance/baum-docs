---
icon: comments
description: The Baum you talk to. Wallets, swaps, launches, copy trading and agents of your own, in a chat.
---

# Baum Agent

Baum Agent is the Baum you message. Tell it what you want in plain words, and it does the onchain work: makes you wallets, prices and places swaps, launches tokens, copies traders, and runs agents of your own that trade while you're away.

It lives in Telegram as [@BaumReviewBot](https://t.me/BaumReviewBot). Text and SMS are coming soon.

{% hint style="danger" %}
**The real bot is exactly [@BaumReviewBot](https://t.me/BaumReviewBot).** Baum will never DM you first, ask for your seed phrase in a group, or ask you to send funds to "verify" anything. See [Stay safe](../official-links.md#stay-safe).
{% endhint %}

## Getting in

Baum on Telegram is **invite only**. You get in with a referral code from someone who already uses Baum:

* Open a friend's invite link. It looks like `t.me/BaumReviewBot?start=ref-CODE`.
* Or open the bot and paste a code into the chat.
* Broker holders and reservers get in by connecting their wallet at [baumai.xyz/broker](https://baumai.xyz/broker). See [Quickstart](../quickstart.md).

No code? Baum tells you how to apply.

## How it works

* **Ask in plain words.** "Buy $20 of BAUM", "what do I hold", "copy this wallet", "launch an agent that buys ETH every Monday". Commands such as `/wallet` work too. `/help` lists them.
* **Nothing moves until you confirm.** Baum shows you every trade, launch or agent before it happens, with **Confirm** and **Cancel** buttons. Agents and automatic orders ask once, then run inside the rules you confirmed, and Baum messages you every time they act.
* **Your wallets, your keys.** Baum makes you a wallet on each chain it trades and keeps the keys encrypted. `/wallet export` gives you a key at any time, and `/wallet <private key>` adds a wallet you already have.
* **One conversation.** `/reset` makes Baum forget the chat. It doesn't touch your wallets.

{% hint style="warning" %}
**`/disconnect` deletes every wallet key Baum holds, and it can't be undone.** Baum asks first. Export your keys, or move your funds out with `/disconnect send <address>`, before you confirm.
{% endhint %}

## In this section

| Page | What's in it |
| ---- | ------------ |
| [What Baum Agent can do](what-it-can-do.md) | Wallets, swaps, launches, copy trading, trading agents, paper trading, alerts and automatic orders |
| [Credits and invites](credits-and-invites.md) | What Baum costs, how to top up, and how referrals work |
| [Baum Harness](../harness/README.md) | How the agents you launch actually run |

Building an app on Baum? See the [Baum API](../api/README.md).
