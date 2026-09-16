# RadBoard Skills

**Radiology labor-market intelligence, inside the AI assistant you already use.**

Five skills that let a practice CEO, CMO or CIO ask plain-language questions about the US
radiology job market and get answers built on live posting data - not on a survey that
shipped nine months ago.

```
"Is $650K competitive for a neuroradiologist in Texas?"
"Why isn't this posting getting applicants?"
"Who else is hiring body imaging in Florida right now?"
"What does closing our night coverage gap actually cost?"
"What changed in our market this quarter?"
```

---

## The problem these solve

Radiology leadership makes seven-figure hiring decisions on the thinnest data of any
specialty. Compensation surveys arrive annually, cost money, and report national medians
that describe nobody's actual market. Meanwhile the question in front of a CEO is specific:
*this* subspecialty, in *this* state, against *these* competitors, this week.

RadBoard tracks active radiology job postings across every US state and the District of
Columbia - title, employer, location, subspecialty, advertised range, partnership track,
vacation, sign-on, ownership type. These skills put that data behind natural-language
questions.

## The five skills

| Skill | The question it answers |
|---|---|
| **rb-comp-check** | Is our package competitive in the market we are actually hiring in? |
| **rb-posting-audit** | Why is this posting not attracting applicants, and how should it read? |
| **rb-coverage-gap** | What does closing this coverage gap by hiring cost, and how contested is the hire? |
| **rb-rival-radar** | Who is recruiting in our market right now, and what kind of organisation are they? |
| **rb-market-pulse** | What moved in our market since last month? |

## What an answer looks like

> **Q: We're offering $600-700K for a neuroradiologist in Texas. Competitive?**
>
> Your range sits at the **12th percentile** of advertised top-of-range for neuroradiology
> in Texas. Competing postings advertise ranges whose upper bounds run $699K at the 25th
> percentile to $945K at the 75th, with a median of $899K. Your ceiling is about $199K
> below that median.
>
> The non-cash picture matters as much here. **81% of competing postings offer a
> partnership track** - offering one is not a differentiator in this market, it is the
> entry ticket. Your 10 vacation weeks match the market median exactly.
>
> *RadBoard, 4,294 active US radiology postings, as of 2026-09-15. 18 postings in this cut,
> salary disclosed at or above $200,000 on 72.2% of them (n=13). Figures are the top of
> posted salary ranges, not median compensation.*

That last paragraph is not decoration. Every answer carries its sample size, its salary
coverage and its date, because a market number without them cannot be judged.

## Quick start

**1. Connect the RadBoard MCP server** in Claude, ChatGPT, Cursor, or any MCP client:

```
https://zagzsrhbwzhzriypnhqf.supabase.co/functions/v1/mcp
```

Sign in with your RadBoard account. Free to create at [www.radboard.io](https://www.radboard.io).

**2. Install the skills.** Clone this repo into your client's skills directory:

```bash
git clone https://github.com/theVmagnificient/radboard-skills.git
```

Each folder holds a single `SKILL.md`. Copy the ones you want, or take all five.

**3. Ask a question.** The matching skill picks itself up - no commands to memorise.

## What we refuse to do

Most market tools answer every question, because an answer looks more useful than a blank.
These do the opposite where the data does not support a number:

- **Nothing below n=10 gets a price.** Ask about a subspecialty in a state with four
  postings and you get the count and an honest refusal, not a median built on four rows.
- **Salary fields say what they measure.** They are the top and bottom of *advertised*
  ranges, not compensation, and they are named so nobody can quote them as pay.
- **Coverage is always stated.** Roughly half of postings disclose a range at all. Every
  salary figure carries how many did.
- **Widening is visible.** When a state is too thin, the answer widens to the census
  division and says so, rather than passing a regional number off as a local one.
- **Counts and estimates are different claims.** A count of open postings is an
  observation and is always shown. A median is an estimate and can be withheld.

[`DATA-NOTES.md`](DATA-NOTES.md) sets out the full interpretation rules. Every skill reads
it before answering, and it is worth five minutes of anyone's time before they quote a
number from these tools in a board pack.

## Built by

[**xAID**](https://www.xaid.ai) alongside [**RadBoard**](https://www.radboard.io).

xAID produces full templated CT reports, ready for a practice's own radiologist to review
and sign, at the price of narrow AI. Reports are validated by European radiologists; the
client's radiologist remains the interpreting physician of record.

We built these because we kept answering the same questions by hand for the groups we work
with. They are more useful in your hands than in ours.

## Contributing

Issues and pull requests welcome - particularly on output formatting. If you have reshaped
one of these to fit how your board actually reads numbers, that version is probably better
than ours.

## Licence

MIT.
