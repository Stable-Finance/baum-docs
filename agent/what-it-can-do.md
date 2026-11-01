---
icon: list-check
description: Everything you can ask Baum Agent to do today.
---

# What Baum Agent can do

Ask in plain words. The commands below are shortcuts, and `/help` lists them all.

## Wallets

Baum makes you a wallet on each chain it trades, Solana and Robinhood Chain, the first time you need one.

* **See them:** "what are my wallets", or `/wallet`.
* **Make more:** `/wallet new <solana|evm>`. Name one with `/wallet name <address> <name>` so you can trade from it by name.
* **Bring your own:** `/wallet <private key>`. Only send a key in your private chat with Baum, never in a group. Baum deletes the message after reading it.
* **Take a key back:** `/wallet export [address]`.
* **Fund:** `/fund` adds ETH or SOL. Baum can also bridge from Base, Ethereum, Arbitrum, Optimism, BNB Chain and Polygon.
* **Move between your wallets:** `/send` is a plain transfer, so the two wallets end up linked onchain. `/split` moves ETH through an exchange so nothing onchain links them. It can't be reversed.
* **Check:** "what do I hold" shows every token with live prices. Baum can also show what you paid for a position.

## Swaps

* **Buy and sell** any token on Solana or Robinhood Chain: "buy $50 of BAUM", "sell half my SOL into USDC". Baum looks the token up, prices the trade for its exact size, and shows it to you with **Confirm**.
* **Sell whole positions:** `/sell <tickers> [into <asset>] [from <wallet>]`.
* **Many wallets at once:** the same buy from several wallets, or any mix of orders across wallets, on one confirmation. Baum can send them all at once or one by one.
* **Price impact limit:** set the most price impact you'll accept, and Baum won't fill past it.

{% hint style="danger" %}
**Baum prices a swap. It does not vet a token.** Tickers aren't unique, and a token launched this morning can take your money and not give it back. Check the contract address and keep sizes to what you'd be fine losing.
{% endhint %}

## Launches

* **Launch a token on Pons** from your own wallet: send `/launch`, or just say you want to launch. Baum asks for the name, ticker and picture, then shows the launch for you to confirm.
* **Bundled launches:** `/bundle` launches with other people's money in the opening buy. Baum tells its users, and the launch goes 24 hours later. `/bundle status` shows where yours are and the link to share.
* **Creator rewards:** see what your launches have earned, claim fees, and choose how much of your creator rewards buys you Baum credits with `/rewards`.

## Copy trading and copy agents

A **copy agent** buys and sells when the wallets it copies do, inside limits you set. Each one can trade from its own wallet or from your main wallet.

* **What it can copy:** a trader off the [leaderboard](https://baumai.xyz/leaderboard) (`trader:<username>` or `trader:top`), an AI agent's wallet (`agent:<address>`), a wallet tracked on Fomo (`fomo:<handle>`), or a member of Congress (`congress:<name>`).
* **Set it up:** "copy this wallet", or `/copy add <source> [$amount | match]`. `match` spends the same share of your wallet as the source spent of theirs.
* **Limits:** amount per buy, most on one buy, most a day, maximum price impact, pause at a loss, and skip tokens with heavy insider holdings. `/copy set <limit> <value>` changes one. Changes apply to future copies, all copies, or the ones you pick.
* **Confirm once.** A copy agent doesn't trade until you tap **Confirm**. Then it runs without asking and messages you each time.
* **Stop any time:** "stop copying X", `/copy pause`, `/copy resume` or `/copy stop`. Nothing already bought is sold.

You can have up to 5 copy agents, each copying up to 10 sources.

**Just want to hear about trades?** `/follow fomo <handle>`, `/follow trader <name>` or `/follow <member of Congress>` tells you when they trade, and `/mirror` offers the same trade. `/pelosi` shows Nancy Pelosi's disclosed portfolio and can buy the whole basket on one confirmation.

## Trading agents

A **trading agent** has its own new wallet, a name, and rules it follows on its own after one **Confirm**. Its trades rank on agent leaderboards as that agent.

* **Launch one:** "launch an agent". Baum asks for a name, which tokens, how much and how often, a question or two at a time.
* **Today's strategy is DCA:** buy (or sell) one to three Robinhood Chain tokens, $1 to $1,000 each round, paying in ETH from the agent's wallet. Run it every day, every few days, on a weekday each week, several times a day, or every N minutes (at least 5).
* **Coming:** trencher, momentum and RWA agents.
* **Fund it:** a new agent's wallet starts empty. Baum offers to fund it privately so it isn't linked to your main wallet onchain, or you can send ETH to it.
* **Manage:** `/agents` lists them. `/agents stop <name>` stops one, and its wallet and funds stay yours. `/agents username <name> <new name>` renames it. Its slug, like `frank-oak`, never changes.

You need a username first (`/username <name>`), because an agent's slug says who made it. You can run up to 3 agents at once. See [Baum Harness](../harness/README.md) for how they run.

## Paper trading

Practice with pretend money at real prices.

* **Start:** "start a paper account" with $1,000, $10,000, $100,000 or $1,000,000. Then "paper buy $500 of ETH".
* **Honest results:** every paper trade is priced at the real market for its exact size, less Baum's fee and network cost. Results are measured against holding BTC by default.
* **Paper agents:** launch an agent or an automatic order on paper to test a strategy before it touches real money.
* **Publish:** make a paper strategy public at `baumai.xyz/paper/<id>`, on the paper leaderboard if you like. Others can copy it into their own paper account.

## Alerts and automatic orders

* **Price alerts:** "tell me if BAUM goes above $0.0002".
* **Stop-loss and take-profit:** sell a whole position when the price falls or rises to a level, in dollars or percent.
* **Recurring buys and sells:** "buy $20 of ETH every Monday", "DCA $10 a day into SOL".
* **Grid:** buy at evenly spaced lines in a range and sell each lot one line up, over and over.

Automatic orders work on any token on Solana or Robinhood Chain. You confirm each one once, and Baum messages you every time it acts. "Cancel my stop loss" cancels one straight away.

## Liquidity

See your Uniswap v4 positions on Robinhood Chain: range, uncollected fees, what each has earned and its fee APR. Baum can open, add to, collect from, rebalance and close positions in pools it manages, each on a confirmation.

## Account and sharing

* `/username` is your name on baumai.xyz and the leaderboard.
* `/account` sends a one-time link to your account page on baumai.xyz, no wallet needed.
* `/email <address>` links an email.
* `/share` makes a public link to your portfolio: a snapshot, or live for 7 days.
* Baum makes win cards and LP cards you can post on X.
* **Sign in to apps built on Baum:** "sign me in to <app>" sends a one-time link that signs you in with your Baum account.
* `/robinhood` connects a Robinhood account.
* `/report <what went wrong>` tells the team.

## Referrals, invites and credits

See [Credits and invites](credits-and-invites.md).
