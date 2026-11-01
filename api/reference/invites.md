---
icon: envelope-open-text
description: Check an invite code someone opened on your site, and count the click.
---

# Invites

People share their Baum referral codes as invite links. If your site has its own invite links (for example `yoursite.example/<code>`), use this endpoint to check a code when someone opens one.

## POST /api/partner/invite

Says whether a code is real and whose it is, and counts one click for it. The click shows up in the code owner's stats, including `invites[].clicks` in [`GET /api/partner/me`](sessions.md#get-api-partner-me). **Free.**

Send it once per new visitor, not on every page load.

### Body

| Field | Required | Meaning |
| ----- | -------- | ------- |
| `code` | Yes | The code from the link |

### Example

```bash
curl -X POST https://baumai.xyz/api/partner/invite \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"code":"ABCD-1234"}'
```

### Response

```json
{ "valid": true, "code": "ABCD-1234", "from": "frank", "held": false }
```

```json
{ "valid": false }
```

| Field | Meaning |
| ----- | ------- |
| `code` | The code as Baum knows it, in upper case |
| `from` | Who it belongs to: the username of the person who shared it, or `null` |
| `held` | `true` when the code doesn't let a newcomer straight in, and they join a waitlist instead |

Then send the person to Baum with the code on a [deep link](../telegram-deep-links.md), such as `ref-ABCD-1234`.

### Errors

| Status | `reason` |
| ------ | -------- |
| `400` | `bad-code` |

Plus the [common errors](../authentication.md#errors).
