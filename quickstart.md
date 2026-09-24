---
icon: rocket
description: From zero to a working Broker in seven steps.
---

# Quickstart

{% hint style="info" %}
**Baum is in private beta.** Beta opens to all Deed Deck holders the week of September 28. Until then, you can get a Broker and get ready.
{% endhint %}

{% stepper %}
{% step %}
### Set up a wallet on Robinhood Chain

Baum and the Deed Deck run on Robinhood Chain. You need a wallet connected to it with some ETH for gas.
{% endstep %}

{% step %}
### Get a Broker

Mint one in the [public mint](deed-deck/mint.md#public-mint) for **0.03 ETH** at [baumai.xyz](https://baumai.xyz), or buy one on [OpenSea](https://opensea.io/collection/baum-deed-deck).

Every Broker comes with its own onchain wallet, seeded with 0.01 USDX, 0.01 mUSDX and 1 BAUM.
{% endstep %}

{% step %}
### Activate it

Activation lets Baum operate your Broker's wallet. It's a one-time fee of **50,000 BAUM** at Levels 1–2, and it gets cheaper as BAUM grows (see [Sunset rule](points-and-levels/sunset-rule.md)).

See [Activation](deed-deck/activation.md).
{% endstep %}

{% step %}
### Fund the wallet

Deposit **USDX, USDG or ETH** into your Broker's wallet from the [Portal](portal/README.md). Baum can only use approved contracts and can only send funds back to you.
{% endstep %}

{% step %}
### Choose what Baum does

Pick one or more [actions](portal/actions.md): hold USDX, provide liquidity to a core pool, swap (one-off, DCA or limit order), or lend USDG.
{% endstep %}

{% step %}
### Earn points and level up

Your Broker earns [points](points-and-levels/README.md) every day, up to 30,000. Lending USDG earns the most: 3 points per $1 per day. Points unlock [levels](points-and-levels/levels.md), which raise your reward weight and lower your fees.
{% endstep %}

{% step %}
### Talk to Baum

Baum is a chat bot. Connect it from [baumai.xyz](https://baumai.xyz) and you can ask it questions, hand it a wallet, follow a trader, and place orders — all from the chat.

See [Messaging Baum](#messaging-baum) below.
{% endstep %}
{% endstepper %}

## Good to know

* **One Broker caps at 30,000 points a day** — about $10,000 of USDG lent. To earn more, add more Brokers.
* **Activation resets when a Broker is sold.** The new owner reactivates. Level and traits stay with the card.
* **Wallet contents travel with the Broker.** Withdraw anything you want to keep before you sell it or send it to the [vault](deed-deck/vault.md).
* **Idle Brokers lose points** — about 3% a week.

## Messaging Baum

Baum answers on Telegram, as [@BaumReviewBot](https://t.me/BaumReviewBot). Both routes below end in the same place: a one-time `t.me` link that opens the chat already tied to your wallet.

It is one conversation, not one per device — `/reset` clears it everywhere. If Baum also reaches you by text, the thread carries over, minus anything that should not travel that way: it will not take a private key over SMS.

### Connecting

Two doors, depending on what you hold.

* **Reserved a Broker.** On [baumai.xyz](https://baumai.xyz), tap **Connect Telegram** beside your wallet. It hands you a one-time link that opens the chat already tied to that wallet.
* **Minted or bought one.** Go to [baumai.xyz/broker](https://baumai.xyz/broker), connect the wallet holding the Broker, and sign a message. No transaction, no gas, no private key — the signature just proves the wallet is yours, and Baum reads the Broker balance off Robinhood Chain itself.

{% hint style="warning" %}
**The wallet and trading commands are for Broker holders.** Baum re-reads the chain rather than remembering an answer, so if the Broker is sold or moved, the commands close again. A reservation on its own is not enough — the Broker has to be minted.
{% endhint %}

### Commands

| Command | What it does |
| ----------------------------- | ----------------------------------------------------- |
| `/help` | The list, and how to stop |
| `/wallet` | Show your wallets — Baum makes you one on each chain |
| `/wallet <private key>` | Add a wallet of your own (Telegram only) |
| `/wallet export [address]` | Hand a key back to you |
| `/wallet forget <address>` | Drop one wallet |
| `/robinhood` | Connect a Robinhood account |
| `/follow fomo <handle>` | Hear when that wallet trades, within seconds |
| `/follow <name>` | Hear when a member of Congress files a trade |
| `/follow <who> $<amount>` | Set what a mirror would buy |
| `/following` | Who Baum is watching for you |
| `/unfollow [who]` | Stop the notifications |
| `/mirror [ticker]` | Propose an order matching the last one |
| `/confirm <code>` | Approve an order Baum proposed |
| `/cancel` | Drop a proposed order |
| `/disconnect` | Remove connected accounts |
| `/reset` | Forget the conversation |

Anything that is not a command is just a question — about the sale, the collection, your Broker, or a connected account.

### Wallets

The first time you need one, Baum makes you a wallet on each chain it trades — Solana and EVM — and holds the keys encrypted, using them only for swaps you confirm. `/wallet` shows them. `/wallet export` hands a key back so you own it outside the chat too, and `/wallet <private key>` imports one you already have; Baum deletes that message after reading it.

Nothing trades until you fund one.

## Example: follow a trader, mirror a trade

Following [frankdegods](https://x.com/frankdegods) and copying a buy, end to end.

{% stepper %}
{% step %}
### Follow the handle

```
/follow fomo frankdegods
```

Baum resolves the handle against Fomo before saving it, and offers the closest matches if it misses. The `fomo` word is required: a bare `/follow frankdegods` looks like a misspelled politician, and guessing wrong would subscribe you to a stranger.

It confirms what you have agreed to — alerts within seconds of a buy, a default mirror of **$100**, and the caution that it prices a swap and nothing else.
{% endstep %}

{% step %}
### Set the size

```
/follow fomo frankdegods $250
```

Anywhere from **$1 to $10,000**. Once you are already following someone, a bare `/follow $250` changes it. This is the amount a mirror spends, not a limit on what you hold.
{% endstep %}

{% step %}
### Fund a wallet

```
/wallet
```

Send something sellable to the address for the chain you expect to trade on. A mirror swaps out of whatever that wallet holds that is easiest to sell for the target token — so an empty wallet means an offer you cannot take.
{% endstep %}

{% step %}
### Wait for an alert

Baum forwards Fomo's own sentence about the trade, with its age and what a mirror would do:

```
frankdegods bought $SNORT ($18K size) — 14s ago.

/mirror proposes swapping $250 into SNORT on Solana, from the
wallet you gave me a key for. You confirm before anything is signed.

I price it and nothing else. I cannot tell you whether this token
can be sold again — a new one can take the money and not give it back.

/unfollow fomo frankdegods to stop these.
```
{% endstep %}

{% step %}
### Mirror it

```
/mirror
```

The order is priced **when you ask**, not when the alert landed — a proposal built at notification time and sat on would be consenting to a price nobody had seen. Baum works out the swap, shows it to you, and hands back a five-character code.

A Fomo alert names one token, so a bare `/mirror` is unambiguous. A congressional filing can list several, and Baum will ask which — `/mirror NVDA` names one.
{% endstep %}

{% step %}
### Confirm

```
/confirm A7K2P
```

That is the only thing that signs anything. `/cancel` drops it instead. Nothing Baum proposes is placed until the code comes back.
{% endstep %}
{% endstepper %}

`/following` shows what is still live. `/unfollow fomo frankdegods` stops that one; a bare `/unfollow` stops all of it.

### When there is no offer

A mirror is not always on the table, and Baum says which reason applies rather than going quiet.

| What you see | Why |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| A sale goes past with no offer | Copying a sale means holding the token already |
| "That one is on Base" | Baum signs swaps on Solana and Robinhood Chain only. Other chains are news, not offers |
| Nothing at all about a small trade | Positions under **$1,000** are below the notification floor |
| "too late for me to offer it as though it were fresh" | The trade is more than **15 minutes** old — an alert recovered after an outage, not an opportunity |
| "I do not have a Solana key" | Baum holds no key for that chain, so it cannot sign. `/wallet` is what changes it |

{% hint style="danger" %}
**Baum prices a swap. It does not vet a token.** There is no liquidity check, no honeypot check and no tax-on-transfer check — a token deployed this morning can take the money and refuse to give it back. The mirror size is a cap on the loss, not a way of avoiding it. Keep it at something you would not mind losing entirely.
{% endhint %}

Baum also goes quiet after **8 messages an hour**, so a busy morning does not become forty notifications. It tells you when it hits the cap rather than simply stopping.
