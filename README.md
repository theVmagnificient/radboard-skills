# RadBoard skills for radiology leadership

Five skills that turn live US radiology job-posting data into answers a practice CEO, CMO
or CIO actually needs. They run inside Claude, ChatGPT, Cursor or any client that speaks
MCP, on top of the RadBoard MCP server.

| Skill | Answers |
|---|---|
| **rb-comp-check** | Is what we are offering competitive in the market we are hiring in? |
| **rb-posting-audit** | Why is this posting not attracting applicants, and how should it read? |
| **rb-coverage-gap** | What does closing this coverage gap by hiring actually cost, and how contested is it? |
| **rb-rival-radar** | Who is recruiting in my market right now, and what kind of organisation are they? |
| **rb-market-pulse** | What moved in my market since last month? |

## Setup

1. Connect the RadBoard MCP server in your client:

   ```
   https://zagzsrhbwzhzriypnhqf.supabase.co/functions/v1/mcp
   ```

   Sign in with your RadBoard account when prompted. Free accounts can create one at
   www.radboard.io.

2. Install the skills. Copy the folders in this repo into your client's skills directory,
   or clone the repo there. Each folder contains a single `SKILL.md`.

3. Ask a question in plain language - "is $650K competitive for a neuroradiologist in
   Texas?" - and the matching skill picks itself up.

## What the data is

Active radiology job postings collected across every US state: title, employer, location,
subspecialty, advertised salary range, partnership track, vacation, sign-on, ownership
type and posting date.

## What the data is not

It is a record of what employers **advertise**, not of what radiologists earn. Salary
figures are the top and bottom of posted ranges, roughly half of postings disclose a range
at all, and any aggregate built on fewer than ten postings is withheld rather than
estimated.

`DATA-NOTES.md` sets out these limits in full. Every skill reads it before answering, and
so should anyone reviewing the output. A market answer without its posting count and
coverage percentage is not an answer.

## Who made this

Built by [xAID](https://www.xaid.ai) alongside [RadBoard](https://www.radboard.io).
xAID produces full templated CT reports, ready for a practice's own radiologist to review
and sign, at the price of narrow AI. Reports are validated by European radiologists; the
client's radiologist remains the interpreting physician of record.

## Licence

MIT. Use them, fork them, change the output format to suit your board pack.
