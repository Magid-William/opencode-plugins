---
description: Pick the best model for a task, or for continuing this session
subagent: false
---

Plan: Go. **Task:** $ARGUMENTS

If the task is empty, recommend the model that should continue this session:
say in one sentence what we are doing and what comes next, then base the picks
on that. If there is no real task yet, ask me.

Scan:
- `opencode models` — only recommend slugs listed there.
- `https://opencode.ai/inference/go/v1/models` — project compactly with
  PowerShell (no raw JSON): input/output price per 1M, context, tools,
  image input, monthly Go limit, peak multipliers.
- `opencode stats --days 1 --models 3` (repeat for 7 and 30) — spend so far
  against the monthly limit. The 5-hour cap is 20% of monthly; the weekly cap
  is 50%.

Free `opencode/*` models have a daily cap, not a Go limit.

Pick exactly three distinct models:
1. **Cheap** — lowest total cost that still finishes without retries.
2. **Balanced** — best capability per dollar.
3. **Best** — strongest for the task, cost ignored.

For each: name, full slug (`provider/model#variant` only if it exists), why,
price per 1M, context, monthly limit and burn so far, main risk. Never invent
a slug, price, limit, or variant.

Output: task line plus the three winners, three tight blocks, then (task mode
only) all available slugs grouped by provider, then `Use:` the balanced pick
and how to switch (`/models` or `--model <slug>`). If we are already on the
right model, say so.
