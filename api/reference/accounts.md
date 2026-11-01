---
icon: user-gear
description: Show and change a signed-in person's Baum profile from your site.
---

# Accounts

Profile and settings screens for your site. These do the same as baumai.xyz/account and the matching Baum commands, for the person a session belongs to. All are **free**, and all need both headers:

```
Authorization: Bearer <key>
X-Baum-Session: <session>
```

See [Sessions](sessions.md). Changes are limited to 30 an hour per person.

| Method | Path | Body | Does |
| ------ | ---- | ---- | ---- |
| `GET` | `/api/partner/account/me` | | Profile, username rules, picture, email, wallets and agents |
| `POST` | `/api/partner/account/username` | `{ "username" }` | Set or change their username |
| `POST` | `/api/partner/account/agent-username` | `{ "agent", "username" }` | Change one of their AI agents' usernames. Its slug never changes |
| `POST` | `/api/partner/account/email` | `{ "email" }` | Set their email. `""` clears it. A new email gets Baum's confirmation email |
| `POST` | `/api/partner/account/avatar` | `multipart/form-data`, field `picture` | Set their profile picture |
| `DELETE` | `/api/partner/account/avatar` | | Remove their profile picture |

## GET /api/partner/account/me

```bash
curl https://baumai.xyz/api/partner/account/me \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..."
```

Everything in [`GET /api/partner/me`](sessions.md#get-api-partner-me), plus:

```json
{
  "usernameChange": { "canChange": false, "changesLeft": 2, "nextChangeAt": "2027-01-15T00:00:00.000Z" },
  "email": "frank@example.com",
  "emailVerified": true,
  "personalWallet": "0x...",
  "walletDetails": [
    { "address": "0x...", "label": null, "agent": null },
    { "address": "0x...", "label": "oak", "agent": { "name": "oak", "slug": "frank-oak", "username": "oak", "status": "active" } }
  ]
}
```

| Field | Meaning |
| ----- | ------- |
| `usernameChange` | Whether they can change their username now. A username can change a few times, 90 days apart |
| `email`, `emailVerified` | Their account email and whether it's confirmed |
| `personalWallet` | The website wallet they linked on baumai.xyz, if any. Baum can't sign for it |
| `walletDetails` | Every EVM wallet Baum holds for them, with AI agents marked |

## Changing things

```bash
curl -X POST https://baumai.xyz/api/partner/account/username \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..." \
  -H "Content-Type: application/json" \
  -d '{"username":"frank"}'
```

```bash
curl -X POST https://baumai.xyz/api/partner/account/avatar \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "X-Baum-Session: q9V..." \
  -F "picture=@me.png"
```

A change answers `{ "ok": true }`. Setting an email also returns `confirmation`, which says whether the confirmation email went out.

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | A sentence: an invalid username or email, or a picture Baum can't use |
| `401` | `signed-out` |
| `404` | `unknown-action` |
| `409` | A sentence: the username is taken or can't change yet, or the account isn't set up for this yet |
| `413` | The picture is over the size limit |
| `429` | `Too many changes. Try again in an hour.` |

Plus the [common errors](../authentication.md#errors).
