---
icon: right-to-bracket
description: Let people sign in to your site with their Baum account, the way other apps use Google.
---

# Sign in with Baum

Every Baum account lives in Telegram, so that is where sign-in happens. Your site never sees a password or a private key. It gets a session and the person's public profile.

## How it works

{% stepper %}
{% step %}
### Your Sign in button opens Baum

Link the button to Baum with an `atp-login-` start parameter and your referral code:

```
https://t.me/BaumReviewBot?start=atp-login-YOURCODE
```

`YOURCODE` is your own Baum referral code. Send `/referral` to Baum to see it. Someone who is new to Baum is recorded as referred by you.
{% endstep %}

{% step %}
### Baum sends a one-time link to your site

Baum replies with a **Sign in** button that opens your sign-in URL with a code:

```
https://yoursite.example/connect-baum?code=Xk3...
```

The code works for **10 minutes** and can be used **3 times**. Telegram often opens links in its own browser first, and **Open in browser** opens the same link again, so one use is not enough. People can also paste the link into a code box on your site.
{% endstep %}

{% step %}
### Your server trades the code for a session

```bash
curl -X POST https://baumai.xyz/api/partner/session \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"code":"Xk3..."}'
```

```json
{
  "session": "q9V...",
  "profile": { "username": "frank", "wallets": ["0x..."], "...": "..." }
}
```

Keep the session on your server, tied to the person's login on your site. It lasts **30 days** and only works with your key.
{% endstep %}

{% step %}
### Read the profile whenever you need it

```bash
curl https://baumai.xyz/api/partner/me \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

The same session works for [account settings](reference/accounts.md) and [copy agents](reference/copy.md).
{% endstep %}
{% endstepper %}

## Set up your sign-in URL

Baum needs to know where to send the code. Sign-in URLs are registered by the Stable team for now: reply to any Baum API email, or ask in the [community chat](https://t.me/BaumChat), with the URL on your site that accepts `?code=`.

Until your URL is registered, `atp-login-` links answer "That site doesn't have sign-in yet."

## What your site sees

The profile has the person's username, the EVM wallets Baum holds for them, their AI agents, a summary of their copy agents, their referral codes with click and sign-up counts, and their profile picture. That's the same information their agents already show in public, plus their own copy settings.

Your site never sees private keys, and it can't move funds. Starting a copy agent or anything else that trades still needs the person to tap **Confirm** in Baum.

See [Sessions](reference/sessions.md) for the full response shape.

## Signing out

```bash
curl -X DELETE https://baumai.xyz/api/partner/session \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

## Errors

| Status | `reason` | What to do |
| ------ | -------- | ---------- |
| `400` | `bad-code` | The code isn't the right shape. Check you passed the whole `code` parameter |
| `410` | `expired-code` | The code is older than 10 minutes, used 3 times, or unknown. Ask the person to sign in again |
| `401` | `signed-out` | The session expired or was signed out. Start sign-in again |
