# geo-barometer-norge

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22837123.svg)](https://doi.org/10.5281/zenodo.22837123)

Published results of the Sitera GEO barometers: how often Norwegian B2B firms are named by
generative AI engines when a buyer asks for a supplier.

Maintained by [Sitera](https://sitera.no), Oslo. Author: Emmanuel Philis (org.nr 937 705 794).
Extracted 18.09.2026 from the published barometer pages.

Protocol: [sitering-metoden](https://github.com/sitera-no/sitering-metoden).

---

## What this is

Thirteen sector barometers, published on sitera.no between June and September 2026, in
machine-readable form. Four engines — ChatGPT, Gemini, Claude, Perplexity — asked a frozen set
of buyer questions in logged-out browser sessions, most sectors in two draws on separate days.

**This is the published aggregate, not the raw measurement matrix.** Each barometer page reports
how many cells a firm was named in (`7 av 20`); it does not publish which specific
question × engine cells those were. The cell-level matrices are not in this repository.

---

## Files

| File | Content |
|---|---|
| `sporsmal.csv` | The buyer questions, one row per sector and question |
| `resultater.csv` | The published ranking tables, in long format |

### `sporsmal.csv`

```
sektor;sporsmal_nr;sporsmal
```

60 questions across 12 sectors. **immaterialrett is absent**: its page does not publish its
question set. That is a gap in the source, not in the extraction.

Where a page lists its questions inline in a sentence rather than as a list, they were split on
the separator the page itself uses. Where a page mixes method notes and questions in the same
list, only the questions were kept. Both operations are editorial; anyone re-deriving this file
from the pages should expect to make the same judgement calls.

### `resultater.csv`

```
sektor;rad;kolonne;verdi
```

474 rows. Long format on purpose.

The thirteen pages do not share a table structure. Some publish a single citation count, some
publish T1 and T2 separately, some add a stability column, some add an org.nr column, some rank
with a `#` column and some do not. Normalising them into one wide table would require inventing
values that the pages never published, or silently discarding columns.

So each table is stored as it appears: one row per cell, carrying the sector, the row index, the
column heading **as printed on the page**, and the value. Nothing is renamed, merged or converted.

Known consequences, none of them corrected:

- Column names differ across sectors (`Siteringsgrad`, `Målinger`, `/20`, `Stabile celler`).
- Denominators differ: 20 cells in most sectors, 8 in immaterialrett.
- Some rows group several firms in one cell, separated by `·`. That is how the pages publish the
  lower tiers, and splitting them would change what was published.
- `ai-synlighet` has no numeric score column — its page reports which engines named each actor.
- `it-saas` has no table on the page and therefore no rows here.
- In `immaterialrett`, the firm cell contains an inline annotation glued to the name
  (`Zacco NorwaySitert i fire av fire motorer`). That is the page's own markup, preserved.

---

## What these numbers are not

They do not say which firm is best. They count how often engines named it, on a stated question
set, on stated dates.

They say nothing about firms that do not appear. An absence in one measurement is not a claim.

A different draw would give different numbers. Between two consecutive days, firms moved by two
to three cells with nothing changed on their websites. That volatility is the reason the protocol
requires two draws before a name is published, and the reason no figure here should be read as a
position rather than a frequency.

---

## Source

Each row derives from a page under `https://sitera.no/geo-barometer-*`. The pages carry the
method line, the measurement dates, the engine versions used on the day, and the publication
threshold. Where this repository and a page disagree, the page is authoritative.

## Licence

Data: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Reuse it, including commercially;
credit Sitera and link to the source page.
