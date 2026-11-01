---
icon: ticket
description: What Baum Agent costs, how to top up, and how referrals and invites work.
---

# Credits and invites

## Credits

Baum Agent runs on **credits**. A reply costs credits, and so do a few things that keep running or touch the chain, such as setting an alert, receiving one, launching a token, or opening and closing an LP position.

* **Broker holders pay less.** With a [Broker](../deed-deck/README.md) connected, most things cost one credit. Everyone else pays more.
* **`/costs`** lists what everything costs right now. Prices can change.
* **`/credit`** shows your balance and how many replies it buys. `/credit alerts on` warns you when you're running low.

Trades also pay Baum's normal swap fee. That is separate from credits.

### Getting credits

| How | What happens |
| --- | ------------ |
| `/fund` | Add ETH or SOL to your wallet. 10% of it, up to $5, becomes credit, and the rest stays yours |
| `/topup <amount>` | Burn BAUM you already hold for credits |
| `/rewards` | Let part of your launches' creator rewards buy you credits |
| `/sponsor` | If you came to Baum through an app that sponsors its users, see the credits it gave you. `/sponsor more` asks for more, when the app takes requests |

At zero credits Baum stops replying until you top up. Broker holders included.

{% hint style="info" %}
These credits are for using Baum yourself. Apps that build on Baum buy separate [API credits](../api/credits.md).
{% endhint %}

## Invites

Baum on Telegram is invite only. Anyone with a valid referral code gets in, so the way to bring a friend is to share yours.

## Referrals

`/referral` shows your referral codes, one for each wallet in your Baum account, each with a Telegram link and a website link to share. It also shows how many people joined through them, and the fees Baum has made from those people with your 10% share. Baum shows the current terms alongside.

* **Share a link:** Baum gives you a message ready to forward.
* **Share a token:** `/referral <ticker or address>` makes a link to trade that token, with your code on it.
* **First code wins:** an account keeps the first referral code it arrives with.

The Telegram link looks like:

```
https://t.me/BaumReviewBot?start=ref-YOURCODE
```

Building something that sends people to Baum? See [Telegram deep links](../api/telegram-deep-links.md).
