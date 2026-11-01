---
icon: gears
description: The runtime that creates and runs autonomous agents for Baum's users.
---

# Baum Harness

Baum Harness is the runtime behind the agents you launch in [Baum Agent](../agent/README.md). When you say "launch an agent", Baum Agent drafts it with you. The harness then gives the agent a wallet, an identity, rules and a schedule, and runs it.

It is the same harness Baum uses for its own work across Stable (see [Introduction](../README.md)), opened up so anyone can have agents of their own.

## What an agent is

Every agent the harness runs has five parts.

| Part | What it means |
| ---- | ------------- |
| **Its own wallet** | A new EVM wallet made for the agent and named after it, so its trades are its own record. It starts empty. The key is held encrypted like your other Baum wallets, and the wallet and its funds are always yours |
| **An identity** | A name, a username you can change, and a permanent slug from your username and its name, like `frank-oak`. Apps built on Baum use the slug for the agent's page |
| **A strategy** | What it trades and why. It is also the category the agent is listed under on agent leaderboards |
| **Limits** | What it may spend and how: tokens, amount per round, price impact, and for copy agents, daily caps and a pause at a loss |
| **A schedule** | When it acts: every day, every few days, on a weekday each week, several times a day, or every N minutes, in your timezone. It can stop after a set number of rounds |

## How it runs

{% stepper %}
{% step %}
### Draft

Baum Agent asks what it needs to know, a question or two at a time, and looks up every token's address.
{% endstep %}

{% step %}
### Confirm once

You see the whole agent, including its wallet, rules and schedule, under one **Confirm**. Confirming is the permission for everything the agent then does on its own. Baum Agent can propose an agent, but only you can confirm one.
{% endstep %}

{% step %}
### Run

The harness checks every minute for agents and orders that are due, and acts inside the rules you confirmed. It messages you every time an agent trades.
{% endstep %}

{% step %}
### Rank

The agent's trades are tracked to its wallet and show on the [leaderboard](https://baumai.xyz/leaderboard) and on agent platforms built on Baum, under its name and strategy.
{% endstep %}

{% step %}
### Stop

`/agents stop <name>` stops an agent. Nothing it bought is sold, and its wallet and funds stay yours.
{% endstep %}
{% endstepper %}

## What runs on it today

| Kind | What it does |
| ---- | ------------ |
| **Trading agents** | DCA: buy or sell one to three Robinhood Chain tokens, $1 to $1,000 each round, on a schedule. Trencher, momentum and RWA strategies are coming |
| **Copy agents** | Buy and sell when the wallets they copy do, within per-trade, daily, price impact and loss limits |
| **Automatic orders** | Stop-losses, take-profits, recurring buys and sells, and grids, on Solana and Robinhood Chain |
| **Paper agents** | Any of the above with pretend money at real prices, to test a strategy before it touches real funds |

For now, one person can run up to 3 trading agents and 5 copy agents.

## Guardrails

* **Rules are fixed at Confirm.** An agent can't trade tokens, amounts or times you didn't confirm. Changing its limits is your choice, made through Baum.
* **Every action is reported.** You get a message each time an agent or order acts.
* **Price impact limits apply.** Fills honour your price impact limit.
* **You can always leave.** Stop an agent any time, and export its wallet's key with `/wallet export`.

## For developers

Today the harness runs agents for Baum's users, launched through Baum Agent. It may open to developers later, so you could bring your own strategies to it. There is no date for that yet.

Until then, apps can already build around Baum's agents with the [Baum API](../api/README.md): look agents up with [`/api/partner/agent`](../api/reference/agents.md), rank them with the [leaderboard](../api/reference/leaderboard.md), and send people to launch or copy one with [Telegram deep links](../api/telegram-deep-links.md).
