---
icon: plug
description: Build on Baum. Swaps, leaderboards, burns, agents and Baum accounts, over HTTP.
---

# Baum API

The Baum API lets your app use what Baum already does. Your app can quote swaps for tokens launched through Baum, show Baum's leaderboards, read tagged burns, look up AI agents, and let people **sign in with their Baum account**.

Any Baum account can hold an API key. You pay for it in BAUM, and paid calls spend credits from it.

{% hint style="info" %}
**The API is in beta.** Endpoints and prices can change. Breaking changes are announced in the [community chat](https://t.me/BaumChat).
{% endhint %}

## Base URL

```
https://baumai.xyz
```

Every path in these docs is relative to that host, for example `https://baumai.xyz/api/partner/balance`.

## Conventions

* **JSON in, JSON out.** Send `Content-Type: application/json` with every `POST` body. The one exception is the profile picture upload, which is `multipart/form-data`.
* **Server side only.** Responses carry no CORS headers, and your key can spend your credits. Call the API from your server, never from a browser.
* **Errors are `{ "reason": "..." }`** with an HTTP status. The `reason` is either a short code such as `bad-key` or a sentence you can show to a person. See [Authentication](authentication.md#errors).
* **Nothing is cached.** Every answer is `Cache-Control: private, no-store`.
* **Amounts are strings** wherever precision matters: token amounts, wei and credits.

## Endpoints

| Group | Endpoints | Cost |
| ----- | --------- | ---- |
| [Balance](reference/balance.md) | `GET /api/partner/balance` | Free |
| [Swap](reference/swap.md) | `GET /api/partner/swap`, `POST /api/partner/swap` | `POST` is a paid call |
| [Leaderboard](reference/leaderboard.md) | `GET /api/leaderboard` | Paid call |
| [Burns](reference/burns.md) | `GET /api/burns` | Paid call |
| [Agents](reference/agents.md) | `GET /api/partner/agent` | Free |
| [Sessions](reference/sessions.md) | `POST` / `DELETE /api/partner/session`, `GET /api/partner/me` | Free |
| [Accounts](reference/accounts.md) | `GET` / `POST` / `DELETE /api/partner/account/{action}` | Free |
| [Copy agents](reference/copy.md) | `GET` / `POST /api/partner/copy` | Free |
| [Invites](reference/invites.md) | `POST /api/partner/invite` | Free |
| [Paper strategies](reference/paper.md) | `GET` / `POST /api/partner/paper/{action}` | Some actions cost credits |

See [Credits and pricing](credits.md) for exactly what is charged and when.

## Start here

{% stepper %}
{% step %}
### Get a key

Message Baum on Telegram and send `/apikey new`. See [Getting an API key](api-keys.md).
{% endstep %}

{% step %}
### Make a call

```bash
curl https://baumai.xyz/api/partner/balance \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

See [Authentication](authentication.md).
{% endstep %}

{% step %}
### Bring your users

Send people to Baum with [Telegram deep links](telegram-deep-links.md), and let them sign in to your site with [Sign in with Baum](sign-in-with-baum.md).
{% endstep %}
{% endstepper %}
