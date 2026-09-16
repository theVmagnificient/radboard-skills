# Reading RadBoard data without overstating it

Every skill in this repo depends on these rules. They exist because the underlying data
has specific, known limits, and a confident answer built on a thin slice is worse than
no answer at all.

## The salary fields do not mean what their names suggest

RadBoard salary metrics are computed from the **top of each advertised range**.

- `salary_max_median` is the median of the highest number each employer advertised.
- `salary_min_median` is the median of the lowest.
- Neither is average pay, and neither is what a radiologist takes home.

Say "top of advertised range" or quote both bounds as a range. Never say "average salary",
"median compensation", or "radiologists earn". If you report a single number where a range
is available, you have already misled the reader.

Roughly half of postings disclose salary at all. Every response carries `coverage_pct` and
`n_with_salary` - state them whenever you state a salary figure.

## Sample size is a hard gate, not a caveat

Any aggregate below **n=10** is returned as `insufficient_data: true` with its real count.
Do not work around this. Do not average adjacent groups to manufacture a number. Do not
report the count as though it were a price.

If the API widened the geography to find enough data, the response says so in `geo_level`
and `widened_from`. When that happens, tell the reader: "not enough postings in Wyoming,
so this is the Mountain division" is a useful answer. Silently presenting a division
number as a state number is not.

## Counts and prices are different kinds of claim

A count of open postings is an observation - report it at any sample size. A median is an
estimate - it is suppressed below n=10. `by_ownership` returns `open_count` for every
bucket and suppresses only the salary median. Use counts freely, prices carefully.

## What the data is, and is not

- **Is:** active radiology job postings in every US state, as collected by RadBoard.
- **Is not:** a census of radiologists, of filled positions, or of actual compensation.
- Subspecialty is derived from the posting title, not from a field the employer filled in.
- Postings that are training seats (fellowship and residency positions) are excluded from
  demand figures. "Fellowship trained preferred" is a job, not a training seat.
- `locum` is derived from the posting text. Do not use any raw `is_locum` flag.

## Canonical subspecialties

`body/abdominal`, `breast`, `neuroradiology`, `ir`, `msk`, `chest/cardiothoracic`,
`nuclear medicine`, `pediatric`, `cardiac`, `emergency`, `general`.

Short forms are accepted on input: `neuro`, `peds`, `chest`, `body`, `nuclear`.
A handful of labels have no canonical home and keep their own names - `teleradiology`
is a work model rather than a subspecialty, so treat it as such.

## Shared filter object

```
states[], subspecialties[], is_remote, ownership_type[], is_academic,
exclude_locum (default true), posted_within_days, salary_floor (default 200000)
```

Unknown keys are rejected rather than ignored, so a typo fails loudly instead of quietly
returning a national number. If a call is rejected, fix the key - do not drop the filter.

## Always show the provenance

Every response carries a `source_note`. Print it, verbatim, at the end of any answer that
uses these numbers. It states the posting count, the salary coverage, the date of the
newest posting included, and the salary floor applied. A reader who cannot see those four
things cannot judge the answer.
