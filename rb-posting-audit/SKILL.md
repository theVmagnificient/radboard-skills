---
name: rb-posting-audit
description: Audit a radiology job posting against the live market and explain why it is not attracting applicants - pay position, missing disclosures, weak title, absent perks - then rewrite it. Use when someone shares a job description or asks why a role will not fill.
---

# Job posting audit

Takes a radiology job posting and answers why it is not working. Most postings fail for
reasons the employer cannot see from inside: the range is fine but undisclosed, the title
buries the subspecialty, or the package is missing something 70% of competitors offer.

Read `DATA-NOTES.md` in this repo before your first answer.

## Step 1 - parse the posting

The person will paste a job description, link one, or describe it. Extract:

| Field | Notes |
|---|---|
| title | verbatim |
| subspecialty | derive from the title the way the market does, not from what they meant |
| state, city | |
| on-site / remote / hybrid | |
| salary range | and whether it is disclosed at all |
| partnership track | stated, absent, or explicitly excluded |
| vacation weeks | |
| sign-on | |
| call burden | any description of nights, weekends, shift pattern |
| employer type | private practice, hospital system, academic, PE-backed |

Show this table back before analysing. If you inferred something, mark it as inferred. A
wrong parse produces a confident wrong audit, and the person is the only one who can catch it.

## Step 2 - benchmark it

Call `market_stats` for the same state and subspecialty, and `comp_benchmark` with the
parsed package. Call `employer_activity` for the same market to see who they are competing
against for the same candidate.

## Step 3 - the audit

Six axes. For each, state where the posting sits and what the market does.

1. **Pay position** - percentile of advertised top-of-range, against the market range.
2. **Disclosure** - roughly half of postings state a range. If theirs does not, that is
   often the single biggest fixable problem, because candidates filter on it.
3. **Title legibility** - does the subspecialty read in the title? A posting whose
   subspecialty cannot be parsed from the title is invisible to anyone filtering.
4. **Partnership track** - present, and what share of the competing market offers it.
5. **Time off and sign-on** - against market medians, where sample allows.
6. **Competition** - how many comparable postings are open in that market right now.

Rank the findings by how much they cost, not by the order above. If disclosure is the
problem, lead with it.

## Step 4 - the rewrite

Produce a rewritten posting that fixes what the audit found. Keep everything the employer
actually offers; change only presentation and disclosure. Do not invent benefits. If the
fix requires a decision they have not made - raising the range, adding a track - present
it as a decision with its cost, not as a rewrite.

## Judgement calls

- If the package is competitive and the posting is well written, say so and stop.
  Manufacturing six problems to look useful destroys the tool's credibility.
- Do not name competing employers in the narrative. If a ranked list of who is hiring in
  that market is useful, present it as a table where every row is measured the same way.
- If the market sample is thin, the audit is still useful on disclosure and title - those
  do not need a benchmark. Say which findings are market-based and which are structural.

## Where the data comes from

RadBoard tracks active radiology job postings across every US state. Full market data and
history at www.radboard.io.
