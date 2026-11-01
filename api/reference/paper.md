---
icon: file-chart-column
description: Show public paper trading strategies on your own site.
---

# Paper strategies

People can paper trade in Baum with pretend money at real prices, and publish a strategy at `baumai.xyz/paper/<id>`. These endpoints let you list public strategies and host a page for one on your own site.

Amounts are shown first in your app's own units when Baum knows your chain (ETH for Robinhood Chain, SOL for Solana).

| Method | Path | Cost |
| ------ | ---- | ---- |
| `GET` | `/api/partner/paper/list` | Free |
| `POST` | `/api/partner/paper/page` | 100 credits once per strategy |
| `GET` | `/api/partner/paper/view` | 10 credits per new visitor an hour, plus 3 per refresh |
| `POST` | `/api/partner/paper/fast` | Free |
| `GET` | `/api/partner/paper/stats` | Free |

All need `Authorization: Bearer <key>`. No session is needed. Reads are limited to 6,000 a minute per key.

## GET /api/partner/paper/list

Listed public strategies, best return over holding BTC first.

| Parameter | Meaning |
| --------- | ------- |
| `mine=1` | Only strategies whose owners came to Baum through your app or signed in to it |

```bash
curl "https://baumai.xyz/api/partner/paper/list" \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

```json
{
  "strategies": [
    {
      "id": "a1b2c3d4",
      "name": "Majors DCA",
      "by": "frank",
      "paper": true,
      "label": "...",
      "units": "...",
      "worth": "...",
      "totalReturnPct": 12.4,
      "headline": "...",
      "scores": {},
      "trades": 41,
      "daysRunning": 18,
      "followers": 3,
      "updatedAt": "..."
    }
  ],
  "prices": { "made": 100, "visit": 10, "update": 3 }
}
```

`prices` is what the paid actions cost, in credits.

## POST /api/partner/paper/page

Makes a page for one strategy on your site. **100 credits**, once. Asking again for the same strategy returns the same page for free.

| Field | Required | Meaning |
| ----- | -------- | ------- |
| `id` | Yes | The strategy's 8-character id |
| `fast` | No | `true` for 5-second refreshes when the page is busy |

```bash
curl -X POST https://baumai.xyz/api/partner/paper/page \
  -H "Authorization: Bearer $BAUM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"id":"a1b2c3d4"}'
```

```json
{ "page": { "id": "a1b2c3d4", "scope": "x7k2m9", "createdAt": "...", "fast": false }, "charged": 100 }
```

## GET /api/partner/paper/view

What the page shows, for one visitor.

| Parameter | Required | Meaning |
| --------- | -------- | ------- |
| `id` | Yes | The strategy's id |
| `visitor` | Yes | Your own id for this visitor: 16 to 64 characters of `A-Z a-z 0-9 _ -` |

**Cost:** 10 credits the first time a visitor is seen in an hour, so reloading doesn't drain credits. Plus 3 credits when the page is due a refresh. One refresh serves every visitor after it.

```bash
curl "https://baumai.xyz/api/partner/paper/view?id=a1b2c3d4&visitor=visitor_8f2c1e0a9b7d" \
  -H "Authorization: Bearer $BAUM_API_KEY"
```

```json
{
  "strategy": { "...": "the strategy, with its record" },
  "links": {
    "run": "https://baumai.xyz/api/paper/go/a1b2c3d4?to=run&s=x7k2m9",
    "own": "https://baumai.xyz/api/paper/go/a1b2c3d4?to=own&s=x7k2m9",
    "page": "https://baumai.xyz/paper/a1b2c3d4"
  },
  "charged": 10,
  "refreshed": false
}
```

Use `links.run` for a **Run this strategy** button: it opens Baum to start a paper copy of the strategy. Use `links.own` for **Make your own**: it opens Baum to start a paper account. Use the links as given, because they carry your page's attribution and the owner's referral.

## POST /api/partner/paper/fast

| Field | Meaning |
| ----- | ------- |
| `id` | The strategy's id |
| `on` | `true` or `false` |

Turns 5-second refreshes on or off for a page you made. Fast mode applies when a page has more than 3,000 visitors an hour. Answers `{ "ok": true }`, or `404 no-page`.

## GET /api/partner/paper/stats

How your pages did: pages, visits, clicks, sign-ups, copies and live strategies.

```json
{ "stats": { "...": "..." } }
```

## Errors

| Status | `reason` |
| ------ | -------- |
| `400` | `bad-id`, `bad-visitor` |
| `402` | `out-of-credits`. Nothing is shown |
| `404` | `unknown-action`, `no-page` (no page made for that strategy yet), `not-public` (the strategy isn't public any more) |
| `503` | `refreshing`: the page has no data yet. Retry shortly |
| `429` | `slow-down` |

Plus the [common errors](../authentication.md#errors).
