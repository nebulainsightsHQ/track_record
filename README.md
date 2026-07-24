# Nebula Insights — Public Track Record Ledger

This repository is the tamper-evident public ledger for every model prediction published by
[Nebula Insights](https://nebulainsights.net). The same numbers are displayed (with grading and
context) at [nebulainsights.net/odds/track_record.html](https://nebulainsights.net/odds/track_record.html).

## Why this exists

Anyone can claim a track record. Most sports handicappers do — and quietly delete the losses.
This repo makes that impossible for us:

- **Predictions are committed here _before_ games start.** The commit timestamp is public and
  precedes first pitch. We cannot backdate a prediction.
- **Pre-game files are never edited.** Results land later as *separate* files in *separate*
  commits, so every pre-game snapshot stays byte-frozen forever. Any edit to a published
  prediction would be visible in the git history.
- **You can hold your own copy.** Fork this repo at any time. If our history ever changed,
  your fork would prove it.

Losses are in here permanently, right next to the wins. That is the point.

## Layout

```
baseline/     one-time cumulative exports of the full prediction log (starting state)
mlb/totals/          MLB game total (over/under) projections   — YYYY-MM-DD.json (pre-game), YYYY-MM-DD.graded.json (results)
mlb/moneyline/       MLB win-probability projections           — same pattern
mlb/pitcher_strikeouts/  MLB starting-pitcher strikeout projections — same pattern
```

New sports/markets appear as folders **only when real predictions exist for them** — no empty
scaffolds, no implied records.

## What the numbers are (and are not)

Every row is a **projection, not a pick**. We publish our model's independent number beside the
market's opening line and grade both against the actual result. We do not publish betting advice,
and our own methodology pages state plainly where our models trail the market. Details:
[methodology](https://nebulainsights.net/methodology/).

## Field reference

| Field | Meaning |
|---|---|
| `model` | Which model version produced the row (version history is permanent) |
| `label` | Human-readable description of the projection |
| `proj_value` / `proj_prob` | Our number (value markets / probability markets) |
| `market_value` | The market's opening line for the same thing, when one existed |
| `actual_value`, `result`, `correct`, `error` | Filled by grading after the game — null until then |
| `projected_at` | UTC timestamp the prediction was logged (pre-game) |
| `graded_at` | UTC timestamp the result was recorded |

## Verify it yourself

1. Pick any pre-game file. Check the commit that introduced it (`git log --follow <file>`) —
   the commit is public and its push predates the games inside.
2. Confirm the file was never modified afterward: `git log --all -- <file>` shows one commit
   touching it (grades arrive in a different file).
3. Compare against the live site and feeds at nebulainsights.net — same numbers.

Questions: [nebulainsights.net](https://nebulainsights.net) · nebula.insights.ceo@gmail.com
