# Report formats for publish_report

Every report: `kind`, `title` (under 70 characters, specific), `summary` (1–3 plain sentences shown
on cards), `body` (Markdown: headings, short paragraphs, tables), `symbols` (covered NEPSE symbols).

| kind | when | extra fields |
|---|---|---|
| `daily` | daily update | `score` 0–100 and `score_label` (required, see below) |
| `weekly` | weekly review | `period_start`, `period_end` (YYYY-MM-DD) |
| `monthly` | monthly review | `period_start`, `period_end` |
| `dossier` | one stock in depth | exactly one symbol; replaces the previous dossier for it |
| `decision` | position review of one holding (shown as "Position review") | the symbol; an Analyst's view only if the user asked |
| `note` | check-ups, research, anything else | |
| `alert` | something needing attention soon | keep it short, add an action |

## Portfolio health score (daily reports)

`score` 0–100 weighs: diversification and concentration, gain vs cost, momentum vs NEPSE and
sectors, news risk on holdings, and cash buffer. `score_label` says what drove it in a few words,
for example "Concentrated in hydro; strong momentum". Keep scores comparable day to day: move them
for real changes, not wording.

## Action items

`actions`: up to 5, each `{"text": "...", "symbol": "UPPER", "due": "YYYY-MM-DD", "priority": "high|medium|low"}`.
They show in the app until the user ticks them off, so:

- Point at what to look at, not what to trade: "Review NICA: it closed below the 412 alert you set".
- Check `get_open_actions` first; don't add duplicates.
- High priority only for things that cost money if ignored this week.

Every body opens with `## In short` and 2–4 plain bullets, and follows "How to write for the reader" in
SKILL.md: short sentences, everyday words, each technical term explained the first time, no codes in capitals.

When a scheduled task (not a chat) publishes the report, pass `scheduled: true`: people who chose
"Scheduled reports" in Settings → Notifications get it by email.

## Daily update body outline

```
## In short
- NEPSE rose 1.2% today; your portfolio rose 0.8%.
- NABIL is 3% above the stop you set. Nothing else needs you today.
## Your holdings compared with NEPSE
| Stock | Last price | Today | Compared with its sector |
## News that matters
## Stops and profit targets close to the price
## Worth a look
```

## Position review body outline

```
## In short
- You're up 11% on what you paid, after 14 months.
- It's done worse than other hydropower stocks this month.
## Position and proceeds if sold today
## Points in favour of keeping it
## Points against
## What to watch
## Analyst's view (only when the user asked what you'd do)
Lean: trim a third. Hydro is 38% of the portfolio and UPPER is lagging its sector; would revisit if it
closes back above 280 on rising volume.
```
