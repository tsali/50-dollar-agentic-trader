# Logic Changelog

Every *deliberate* change to the trading logic, with the reasoning and (as data accrues) the **measured effect.** Changes are made rarely and on purpose — not to chase short-term noise.

### v1.0 — 2026-08-07 (inception)
Initial ruleset:
- **Full-universe, active agent-driven selection** — the agent picks and rotates positions across the whole market on its own judgment.
- **Risk framework:** hard stop-loss (−10%) always on; keep dry powder (never fully invested); cap concurrent positions; account floor that halts trading if breached; manual kill switch.
- **Holds allowed** — no forced intraday exit; the agent may hold a position with a documented reason and a trailing stop, or rotate out.

*Effect:* baseline. See [TRADES.md](TRADES.md) / [LOG.md](LOG.md).

### v1.1 — 2026-08-10 — Re-entry discipline
**Change:** if the agent re-buys a ticker it exited within ~5 trading days *and* price is now below the prior exit, it tightens the stop to **3–5%** (instead of the default 10%).
**Why:** after an exit that locked a gain, a cheaper re-buy is rational — but a *failed* re-entry should get a tight loss cap so it can't give back the just-locked profit. (Prompted by observing a real exit → re-buy on the same name.)
**Measured effect:** *TBD — to be filled in after more re-entry cases.*

*Note on scope: the agent runs with **no values filter and no blocklist** — the entire market is fair game. The operator's personal convictions are intentionally kept out of the agent's decision set so the experiment stays clean and unbiased.*

---

**How to read this:** a rule change is logged here *before* it's judged, then revisited weeks later to record what actually happened versus the benchmark. That before/after honesty is the whole point.
