---
icon: book
description: Every Baum API endpoint, by group.
---

# API reference

Paths are relative to `https://baumai.xyz`. Every endpoint needs `Authorization: Bearer <key>`. See [Authentication](../authentication.md).

| Group | Method and path | Session | Cost |
| ----- | --------------- | ------- | ---- |
| [Swap](swap.md) | `GET /api/partner/swap` | | Free |
| | `POST /api/partner/swap` | | One call |
| [Leaderboard](leaderboard.md) | `GET /api/leaderboard` | | One call |
| [Burns](burns.md) | `GET /api/burns` | | One call |
| [Agents](agents.md) | `GET /api/partner/agent` | | Free |
| [Sessions](sessions.md) | `POST /api/partner/session` | | Free |
| | `GET /api/partner/me` | Yes | Free |
| | `DELETE /api/partner/session` | Yes | Free |
| [Accounts](accounts.md) | `GET /api/partner/account/me` | Yes | Free |
| | `POST /api/partner/account/{username, agent-username, email, avatar}` | Yes | Free |
| | `DELETE /api/partner/account/avatar` | Yes | Free |
| [Copy agents](copy.md) | `GET /api/partner/copy`, `POST /api/partner/copy` | Yes | Free |
| [Invites](invites.md) | `POST /api/partner/invite` | | Free |
| [Paper strategies](paper.md) | `GET /api/partner/paper/{list, view, stats}` | | `view` costs credits |
| | `POST /api/partner/paper/{page, fast}` | | `page` costs credits |
| [Balance](balance.md) | `GET /api/partner/balance` | | Free |

"One call" is the per-call price on [Credits and pricing](../credits.md).
