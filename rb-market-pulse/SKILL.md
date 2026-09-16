---
name: rb-market-pulse
description: Period-over-period briefing on a radiology hiring market - how posting volume, advertised ranges, remote share and the employer mix have moved, with new entrants called out. Use when someone asks what has changed in their market, wants a recurring market update, or asks whether hiring is heating up or cooling.
---

# Market pulse

A recurring read on one hiring market: what moved since last period, and by how much.
Built for a leader who wants the same briefing every month rather than a one-off answer.

Read `DATA-NOTES.md` in this repo before your first answer.

## What to collect

1. **Market** - state or states.
2. **Scope** - all radiology, or a subspecialty.
3. **Period** - 30 or 90 days.

If this is a repeat run, keep the same filters as last time. A pulse whose scope drifts
between runs measures the scope change, not the market.

## How to run it

`market_pulse` with the filter object and `period_days`. Read three fields before anything
else:

- `actual_period_days` - if it is shorter than what was asked for, the series does not
  reach back that far. Report the window you actually got.
- `reconstructed_days` and `observed_days` - the series has two kinds of day. Observed days
  were recorded live. Reconstructed days were rebuilt afterwards from when each posting was
  first and last seen, so they are survivorship-biased: a posting that opened and closed
  before collection began cannot appear in them, which understates historical volume.
  Never present a mostly-reconstructed comparison as a measured one.
- `source_note` - print it verbatim at the end.

## How to report it

Five lines, in this order, each with the direction and the absolute change:

1. **Volume** - open postings now against period start.
2. **Advertised ranges** - movement in top-of-range and bottom-of-range medians, where
   sample allows.
3. **Remote share** - percentage point change.
4. **New entrants** - employers with postings this period and none last period.
5. **Biggest movers** - employers whose open count grew most.

Then two sentences of reading. Resist narrating every line - the table already says what
happened. Say what it means for someone recruiting into that market.

## What the series will and will not support

Live collection began on 2026-09-16. Everything before that is reconstructed, and the
response tells you the split for the window you asked for.

That split governs how strongly you can phrase the finding. A window that is mostly
observed supports a statement of fact. A window that is mostly reconstructed supports a
direction with the caveat attached in the same sentence - not in a footnote, and not
dropped because the number is striking. A quarter-over-quarter move computed on 89
reconstructed days out of 90 is an indication, and saying so is the difference between a
figure that survives scrutiny and one that does not.

Requests longer than the available series come back with the longest real window and
`actual_period_days`. Report the window you got, never the one that was asked for.

Never annualise a 30-day movement. Never describe a single period's change as a trend.
Two periods make a comparison; three make a trend.

## Setting it up as a recurring brief

If the person wants this monthly, and their environment supports scheduled tasks, offer to
schedule it with the filters fixed. Keep the output format identical between runs so the
numbers are comparable at a glance - a briefing whose shape changes every month cannot be
skimmed, and an unskimmable briefing gets ignored.

## Where the data comes from

RadBoard tracks active radiology job postings across every US state. Full market data and
history at www.radboard.io.
