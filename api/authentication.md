---
icon: lock
description: Send your key as a bearer token. Add a session to act for a signed-in person.
---

# Authentication

## API key

Every endpoint needs your key in the `Authorization` header:

```
Authorization: Bearer baum_...
```

```bash
curl https://baumai.xyz/api/partner/balance \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

Baum stores only a hash of your key. A key you rotate or revoke stops working at once.

## Sessions

Some endpoints act for one person who signed in to your site with their Baum account. They need two headers: your key and that person's session.

```
Authorization: Bearer baum_...
X-Baum-Session: <session>
```

You get a session from [`POST /api/partner/session`](reference/sessions.md) after a person signs in. See [Sign in with Baum](sign-in-with-baum.md).

A session lasts **30 days** and only works with the key that created it. Another app holding the same session token can't use it.

Endpoints that need a session: [`/api/partner/me`](reference/sessions.md#get-api-partner-me), [`/api/partner/account/*`](reference/accounts.md) and [`/api/partner/copy`](reference/copy.md).

## Errors

Every error is JSON with a `reason`:

```json
{ "reason": "bad-key" }
```

| Status | `reason` | Meaning |
| ------ | -------- | ------- |
| `400` | varies | The request is missing something or a value is out of range. The `reason` says which |
| `401` | `no-key` | No `Authorization: Bearer` header |
| `401` | `bad-key` | The key is unknown, rotated or revoked |
| `401` | `signed-out` | The `X-Baum-Session` is missing, expired, signed out, or from another key |
| `402` | `out-of-credits` | A paid call, and your balance can't cover it. See [Credits](credits.md) |
| `403` | `no-email` | A paid call, and your account has no confirmed email. Send `/email` to Baum |
| `404` | varies | Not found, or an unknown `{action}` |
| `429` | varies | Too many requests. Slow down and retry later |
| `5xx` | varies | Baum couldn't reach the chain or a price just now. Retry |

A refused or failed paid call costs nothing. See [Credits](credits.md#what-a-call-costs).

## Keep your key safe

* Call the API **from your server only**. Responses carry no CORS headers on purpose.
* Don't commit the key to a repository or ship it in an app bundle.
* If a key leaks, send `/apikey rotate` to Baum. The old key stops working immediately.
