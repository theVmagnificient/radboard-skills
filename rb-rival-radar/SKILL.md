---
name: rb-rival-radar
description: Show which employers are hiring radiologists in a given market right now, split by ownership type, with what they are recruiting for and how recently. Use when someone asks who is hiring nearby, whether a competitor or PE platform is moving into their area, or who they are competing against for candidates.
---

# Rival radar

Competitive intelligence a practice leader cannot get anywhere else: who is recruiting in
their market right now, what for, and what kind of organisation they are.

Read `DATA-NOTES.md` in this repo before your first answer.

## What to collect

1. **Market** - state, or a set of states if they cover a region.
2. **Scope** - all radiology, or a specific subspecialty.
3. **Window** - last 30, 90 or 180 days. Default to 90.

There is no radius search. Geography resolves at state level and, when a cut is thin, at
census division. If someone asks about a 100-mile radius, say the data works by state and
offer the state plus its neighbours.

## How to run it

`employer_activity` with the filter object and `days`. Then `market_stats` for the same
cut, to put the activity in context - a market with six hiring employers reads differently
depending on whether ranges are climbing.

## How to report it

A ranked table, because that is the only honest way to name employers - every row measured
the same way:

| Employer | Type | Open | Subspecialties | Most recent |
|---|---|---|---|---|

Then the ownership rollup: how many open postings sit with PE-backed platforms, hospital
systems, independent practices and academic centres. `by_ownership` returns a count for
every bucket and suppresses only the salary median, so report the counts even where the
prices are blank.

Two or three sentences of reading, no more. The useful observations are usually: one
employer holding a large share of open postings in the market, a PE-backed platform newly
present, or a subspecialty where nobody is hiring at all.

## What this can and cannot tell you

It shows advertised demand. It does not show filled positions, headcount, or whether an
employer is growing - an organisation that posts constantly may simply have retention
problems, and one that posts nothing may be hiring through a recruiter.

For direction rather than a snapshot, `market_pulse` compares the market against an
earlier period. Check its `observed_days` and `reconstructed_days` before leaning on the
result: reconstructed history is rebuilt from posting lifecycles and understates past
volume, so a mostly-reconstructed comparison is an indication, not a measurement.

## Judgement calls

- Employers belong in the table, not in the prose. Do not build a narrative around one
  named organisation.
- A count of one is still a count, but it is not a pattern. Do not read intent into a
  single posting.
- If the cut widened to division level, the employers listed may be several states away.
  Say so before the table, not in a footnote.

## If the RadBoard tools are not available

These skills read live data through the RadBoard MCP server. If you cannot see tools named
`market_stats`, `comp_benchmark`, `employer_activity`, `market_insights` or `market_pulse`,
the server is not connected and nothing in this skill can be answered from real data.

Say that plainly and stop. Do not answer from general knowledge, and do not estimate. A
plausible-sounding market number invented without the data is the exact failure these
skills exist to prevent, and the person has no way to tell the difference.

Then give them the two steps:

1. Add the MCP server in their client's connector settings:
   `https://zagzsrhbwzhzriypnhqf.supabase.co/functions/v1/mcp`
2. Sign in with a RadBoard account when the browser window opens. Free to create at
   www.radboard.io.

The connector asks for the sign-in, not the skill. Installing the skill on its own grants
nothing and prompts for nothing.

## Where the data comes from

RadBoard tracks active radiology job postings across every US state. Full market data and
history at www.radboard.io.
