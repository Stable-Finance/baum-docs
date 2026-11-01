---
icon: id-card
description: Trade a sign-in code for a session, read the signed-in person's profile, and sign out.
---

# Sessions

The server half of [Sign in with Baum](../sign-in-with-baum.md). All three are **free**.

## POST /api/partner/session

Trades a sign-in code for a session and the person's profile.

### Body

| Field | Required | Meaning |
| ----- | -------- | ------- |
| `code` | Yes | The `code` from your sign-in URL. 20 to 100 characters of `A-Z a-z 0-9 _ -` |

### Example

```bash
curl -X POST https://baumai.xyz/api/partner/session \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"code":"Xk3..."}'
```

### Response

```json
{
  "session": "q9V...",
  "profile": { "...": "see GET /api/partner/me" }
}
```

The session lasts 30 days and only works with the key that redeemed it.

### Errors

| Status | `reason` | Meaning |
| ------ | -------- | ------- |
| `400` | `bad-code` | Missing or the wrong shape |
| `410` | `expired-code` | Older than 10 minutes, used 3 times already, or unknown |

## GET /api/partner/me

The profile of whoever a session belongs to.

### Headers

| Header | Required |
| ------ | -------- |
| `Authorization: Bearer <key>` | Yes |
| `X-Baum-Session: <session>` | Yes |

### Example

```bash
curl https://baumai.xyz/api/partner/me \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

### Response

```json
{
  "username": "frank",
  "wallets": ["0x...", "0x..."],
  "strategy": { "id": "spot", "name": "Spot traders" },
  "copy": {
    "status": "active",
    "sources": [{ "label": "frank-oak", "ref": "agent:0x...", "sizing": "$25 per buy" }],
    "perTradeUsd": 300,
    "dailyUsd": 10000,
    "agents": 1
  },
  "invites": [{ "code": "ABCD-1234", "aliases": [], "clicks": 12, "accounts": 3 }],
  "avatarUrl": "https://baumai.xyz/api/avatar/0x...?v=1",
  "agents": [{ "name": "oak", "slug": "frank-oak", "wallet": "0x...", "status": "active" }]
}
```

| Field | Meaning |
| ----- | ------- |
| `username` | Their Baum username, the same as on baumai.xyz and the leaderboard. `null` if they haven't set one |
| `wallets` | The EVM wallets Baum holds for them, default first |
| `strategy` | The strategy they're listed under on agent leaderboards, or `null` |
| `copy` | A summary across their copy agents, or `null`. [`GET /api/partner/copy`](copy.md) has the detail |
| `invites` | Their referral codes, with how many times each link was opened (`clicks`) and how many accounts joined through it (`accounts`) |
| `avatarUrl` | Their profile picture, or `null` for initials |
| `agents` | AI agents they launched, running ones first. `slug` is `null` until they have a username |

### Errors

| Status | `reason` |
| ------ | -------- |
| `401` | `signed-out` |

## DELETE /api/partner/session

Signs a session out. Answers `{ "ok": true }`, including for a session that had already ended.

```bash
curl -X DELETE https://baumai.xyz/api/partner/session \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

All three also return the [common errors](../authentication.md#errors).
