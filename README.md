# The $50 Agentic Trader

An honest, public, weekly-tracked experiment: a **~$50 brokerage account traded by an AI agent**, run out in the open so anyone can watch what actually happens.

No hype. No "I turned $50 into $50,000." Just a tiny real account, a simple disciplined strategy, an AI agent executing it, and a public log of every week — wins, losses, and any change to the logic.

## Why

Everyone claims their bot prints money. Almost nobody publishes the honest, boring, week-by-week reality — *including the red weeks.* This is that record: a transparent proof-of-concept of whether an AI agent, given real money and a disciplined ruleset, behaves sensibly over time.

The point isn't to get rich on $50. The point is a **rigorous, reproducible, tamper-evident record.**

## The Thesis

What the experiment *is* — these three things are the point of it:

- **Real money, small stakes** — ~$50 in a real brokerage account. Small enough to be honest, real enough to matter.
- **Full-universe picks, zero values filter** — the agent chooses from the *entire* stock market, with no blocklist and no exclusions. Deliberately: the operator's personal convictions are kept out of the agent's decision set, so the data stays clean and unbiased. The agent may buy things the operator never would. (This is the core of the experiment, not a preference — the whole idea is an *unconstrained* agent.)
- **Rigorous records** — every trade, position, and logic change is logged and versioned in git, with timestamps.

## The Rules It Runs On

These are the guardrails *this* agent happens to use — example choices, not gospel. If you build your own (see [below](#build-your-own-agentic-trader-on-robinhood)), **you can add rules like these, tune the numbers, or swap in your own.** None of them are personal mandates; they're just a sane starting point for a tiny real account:

- **Active, agent-driven management** — the agent picks *and rotates* positions on its own judgment, typically holding a name for a few days before moving on. Every single buy and sell is recorded — see **[TRADES.md](TRADES.md)**.
- **A real risk framework** — hard stop-loss on every position, a cap on concurrent positions, an account floor that halts trading if breached, and a manual kill switch. Boring, but it's what keeps a $50 experiment from doing something stupid. (Set your own thresholds.)
- **Dry-powder rule** — always keep some cash on the side. Never 100% invested.
- **No tinkering on noise** — the *logic* isn't changed to chase short-term results. Any change to the ruleset is deliberate, documented in [CHANGELOG.md](CHANGELOG.md), and its effect measured afterward.

## Current Status (as of 2026-08-18)

- **Started:** 2026-08-07 (~$50)
- **Account value:** ~$49.78 — its first small red, after ~1.5 weeks in the green
- **Open positions:** NVDA and ASTS, plus ~$31 cash as dry powder
- **Activity so far:** ~27 trades across NVDA, PLTR, SMR, ZETA, AA, SMCI, RKLB, NBIS, MU, ASTS — full log in [TRADES.md](TRADES.md)
- **Benchmarks** (vs SPY / QQQ) begin tracking now so we can separate *skill* from *luck.*

See **[TRADES.md](TRADES.md)** for every trade, **[LOG.md](LOG.md)** for the weekly value history, and **[CHANGELOG.md](CHANGELOG.md)** for logic changes.

**Updated automatically every Saturday.** A scheduled job pulls the week's real fills and account value straight from the brokerage, writes a self-contained recap to **[`weeks/`](weeks/)** (one file per week, so nothing bloats), refreshes the summaries above, and commits it. No numbers are typed by hand — the git history *is* the tamper-evident record. Account identifiers and order IDs are never published; only the trade economics are.

## How the Agent Decides

There's no single rigid strategy — **the agent does whatever it judges best for each situation.** It can buy and hold, or actively trade in and out, choosing among different decision logics based on what it reads:

- **Signal screen** — social/reddit hype clusters *plus* technical confirmation: price above a rising 20-day moving average, a multi-day uptrend, momentum/EMA, a catalyst, and enough liquidity — while deliberately avoiding "falling knives."
- **Entry** — buys with a defined stop-loss and a target.
- **Management** — holds and *trails the stop upward* while momentum stays intact, to lock in gains; exits at the target, on a stop, or on a breakdown.
- **Re-entries are deliberate** — if it sells a name high and the price pulls back, it may buy it again lower. Sell-high / buy-low, not indecision.

So far it has held some names and rotated others; nothing held very long-term yet. Every decision and the agent's own rationale is logged — see the reasoning notes in **[TRADES.md](TRADES.md)**.

## How Performance Is Judged

Each week we record total account value and compare it to what the *same money* would have done in **SPY** and **QQQ** over the same period. Beating a plain index over time = signal. Not beating it = also useful data. A strategy that never shows a loss isn't really invested.

## Build Your Own Agentic Trader on Robinhood

Want to run your own? Here's the honest how-to. **(Not financial advice — you can lose money.)**

1. **Fund a small, dedicated account.** Use money you can fully afford to lose — this is an experiment. A separate account keeps the record clean.
2. **Give an AI agent access to trade it.** Robinhood has an API, and there are open MCP servers / SDKs that let an AI agent read positions and place orders. (Search "Robinhood MCP," or use the official API.) Scope it to *one* small account only.
3. **Write the rules down first, then don't break them.** Decide the strategy before you start: what it can buy, buy-and-hold vs. active, how much cash to keep as dry powder, how often it may trade. Put the rules in a file and make the agent follow them.
4. **Keep dry powder.** Never go 100% invested — cash on the side is optionality and a shock absorber.
5. **Log everything, weekly, in git.** Value, holdings, changes. Versioning makes it an honest, tamper-evident record.
6. **Benchmark against an index (SPY/QQQ).** It's the only way to tell skill from just riding the market.
7. **Don't tune on noise.** Two weeks tells you almost nothing. Change the logic only deliberately, and measure the effect afterward.
8. **Publish it.** Public accountability keeps you honest and lets others learn.

## Disclaimer

This is a personal experiment with a tiny amount of money, run by an AI agent for research and learning. **It is not financial advice.** Nothing here is a recommendation to buy or sell anything. Past performance says nothing about the future. You can lose money. Not affiliated with, sponsored by, or endorsed by Robinhood or any company mentioned.
