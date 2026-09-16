---
name: rb-comp-check
description: Benchmark a radiology compensation package against the live US job market by state and subspecialty - base range percentile plus partnership track, vacation and sign-on. Use when someone asks whether an offer or salary band is competitive, what the market pays, or how their package compares to competitors.
---

# Compensation check

Answers one question for a radiology practice leader: **is what we are offering competitive
in the market we are actually hiring in?**

Read `DATA-NOTES.md` in this repo before your first answer. The salary fields do not mean
what their names suggest, and getting that wrong is the fastest way to lose a reader.

## What to collect

You need three things before calling anything. Ask for whichever are missing, in one
message, not one at a time:

1. **Where** - state, or states if they recruit across a region.
2. **What** - subspecialty, or general diagnostic.
3. **The package** - base range, and whether it includes partnership track, how many
   vacation weeks, and any sign-on.

Two optional filters change the answer a lot, so offer them: on-site versus remote, and
whether academic postings belong in the comparison. A private practice benchmarking
against academic salaries will get a misleading picture.

## How to run it

Call `comp_benchmark` with the filter object plus the offer:

```
{ states: ["TX"], subspecialties: ["neuroradiology"], is_remote: false,
  my_salary_min: 600000, my_salary_max: 700000,
  my_partnership_track: true, my_vacation_weeks: 10, my_sign_on_bonus: 50000 }
```

Then call `market_stats` with the same filters to get the surrounding context - who else
is hiring in that market and how the benefits distribute.

If the response comes back `insufficient_data`, or `geo_level` is not `state`, say so
before you say anything else. Offer to widen deliberately: neighbouring states, or the
subspecialty dropped, and show what changes.

## How to report it

Lead with the verdict in one sentence, then the arithmetic. Something like:

> Your range sits at the 12th percentile of advertised top-of-range for neuroradiology in
> Texas. The market's advertised ranges run $612K to $899K at the midpoint; yours tops out
> at $700K, about $199K below the median top-of-range.

Then the part most leaders have never seen - the non-cash comparison:

> Partnership track: you offer it, 81% of competing postings in this cut do too. It is not
> a differentiator here, it is table stakes.
> Vacation: 10 weeks against a market median of 10.
> Sign-on: half of competing postings disclose one at all.

Close with the source note verbatim.

## Judgement calls

- **Never** compress the market into one number when two bounds are available. A range
  against a range is the honest comparison.
- If the offer is above market, say that plainly. A skill that only ever says "you are
  underpaying" is a sales tool, and readers work that out in one use.
- If partnership track is near-universal in their market, the useful advice is that cash
  is doing the differentiating, not the track. Say it.
- Benefits medians are suppressed below n=10 like everything else. A `null` vacation
  median means not enough postings disclosed it, not that the market offers none.

## Where the data comes from

RadBoard tracks active radiology job postings across every US state. Full market data and
history at www.radboard.io.
