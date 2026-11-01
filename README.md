# Where Israel's elected representatives live

The raw tables behind the Knesset locality website and its population/representation analysis. Each election dataset contains the original 120 elected members, without subsequent replacements.

- **2022:** 25th Knesset; election 1 November 2022; historical residence snapshot 28 December 2022; population at 31 December 2022.
- **2026:** 26th Knesset; election 27 October 2026; residence snapshot 1 November 2026; population at 31 December 2024. The supplied research roster records completed-count reporting and notes that formal gazette verification is pending.

The datasets preserve the reviewed project assignments. They contain locality-level residence, electoral list/component, party grouping, coalition grouping, gender, age and age uncertainty, public residence sources, public age sources, administrative classifications and their sources, and the population inputs used by the graphs.

## Download and use

Start with [`data/members-2022.csv`](data/members-2022.csv) and [`data/members-2026.csv`](data/members-2026.csv). Every table has an equivalent JSON array beside the CSV. Use GitHub's **Raw** button or clone the repository to pull the files. Column names are English and values retain the Hebrew used by the project; `_he` marks Hebrew labels. `id` is unique within a cohort; `person_key` links a person across cohorts where a shared profile identity is available.

```python
import json
from pathlib import Path

members = json.loads(Path('data/members-2026.json').read_text(encoding='utf-8'))
```

All CSV files are UTF-8 without BOM. Empty CSV cells and JSON `null` mean missing, unknown or not applicable; they do not mean zero. CSV booleans are `true`/`false`. The rare multi-role source label uses ` | ` between values. Every table row is flat, so CSV and JSON have the same columns.

## Tables

| Folder/file | Content |
| --- | --- |
| `data/members-YEAR.*` | 120 person records, including the facts and Hebrew/English labels displayed by the website |
| `data/english-labels.*` | The website's existing English labels for names, parties and places, keyed using its Hebrew lookup rule |
| `data/residence-sources-YEAR.*` | One row per member/source URL, with source dates, recorded locality claims and primary/supporting/site-display flags |
| `data/age-sources-YEAR.*` | Birth-year or reported-age sources, claim type, verification status and factual basis |
| `data/geography-sources-YEAR.*` | Sources for administrative classification, without spatial assets |
| `data/historical-residences-2022.*` | The supplied original two-column historical residence table, preserving its locality spellings |
| `population/localities-2022.*`, `population/localities-2024.*` | All 1,484 / 1,490 rows from the CBS locality inputs, including localities with no MK and rows with unpublished population |
| `population/districts-YEAR.*`, `population/subdistricts-YEAR.*` | All 7 district and 16 analysis-subdistrict population inputs for each population year |
| `population/national.*` | The two published national population denominators |
| `analysis/locality-counts-YEAR.*` | Counts for all 74 / 75 assigned residence localities, including places without a comparable population |
| `analysis/locality-comparisons-YEAR.*` | All 1,218 / 1,221 positive-population localities used to reproduce rankings, including those with zero MKs |
| `analysis/locality-rankings-YEAR.*` | The four five-row ranking lists used by the graphs |
| `analysis/districts-YEAR.*`, `analysis/subdistricts-YEAR.*` | Regional counts, population shares, expected MK counts and representation indices |
| `analysis/aggregates-YEAR.*` | Check totals by electoral list, component, bloc, coalition status, gender, district, analysis subdistrict and age precision |
| `metadata.json` | Cohort definitions, references, formulas and limitations |
| `schemas.json`, `DATA_DICTIONARY.md` | Exact table schemas and field definitions |

`YEAR` in `data/` and `analysis/` is the election year. `YEAR` in `population/` is the population reference year; the 2026 analysis uses the 2024 population files.

## Definitions and limitations

The 2022 residence assignments come from the original table supplied by the project editor. Individual historical residence claims were not all independently reverified. `historical-residences-2022.csv` is included here as a clean two-column source; its relative reference resolves inside `data/`. Current residence evidence has not been backdated to 2022. The historical snapshot date is not an independently established publication date for every underlying claim. Spelling normalization and the original locality label are both retained.

2022 parties are electoral lists at the election. Religious Zionism, Otzma Yehudit and Noam were elected as one 14-member list; the component is separate. For 2026, `coalition_status` is the project editor's outgoing five-party grouping, as described in `metadata.json`. Administrative labels in the canonical 2022 table were normalized using the 2024 CBS reference; the regional 2022 analysis checked them against the 2022 locality file and found no assignment differences. Historical municipality type is retained where it changed.

`age` is the website's value on **1 November** of the election year. Full birth dates produce exact ages; birth years produce a two-value range. A reported age can establish a range without an exact birth year. Missing ages remain null. The website's supplied `age_verified` flag is preserved; that flag alone does not establish that an age is known. Use `age_precision`, null checks and `birth_year_verification` together. Four 2026 ages are missing, one 2026 birth year has only an unconfirmed open-wiki source, and Itamar Eitam has a reported-age range without an exact birth year. Dates and ranges have not been converted into invented exact values.

Population covers all ages using the CBS resident/Israeli population column specified in each row. The separate foreign-national population column is not part of the analysis. Judea and Samaria uses Israeli-locality population and is treated as one analysis subdistrict. CBS regional values are rounded to 0.1 thousand. Use the published national totals (**9,662,000** for 2022; **9,805,100** for 2024) without renormalizing rounded regional sums. Locality-file totals are not a substitute for national population because some residents live outside localities.

```text
expected_mks = 120 * region_population / national_population
representation_index = 100 * actual_mks / expected_mks
mks_per_100k = actual_mks / locality_population * 100000
```

Representation index 100 means the same share of MKs as the population share. Where supplied, the coalition representation index uses that cohort's coalition count as its denominator.

Locality population and rankings refer to the whole CBS statistical locality. An exact-place ranking omits a place when its separate population cannot be compared with the merged municipality. Population-null places are not treated as empty and are excluded from population-based rankings; they remain in the member and locality-count tables. Ties in MK counts are broken by descending population, then CBS code. The five-largest-cities comparison first selects the five largest cities; it is not a ranking of cities by their per-capita MK count. City classification includes the reviewed 2026 promotion of Givat Zeev.

Residence source freshness and provisional status are retained in the member table. A URL in the sources table records the project's provenance; it does not imply that the source independently confirms a current residence or that every source was independently read. Additional source roles can refer to older or alternative claims. The `displayed_on_site_flag` identifies the sources used in the website's member card.

The public export intentionally excludes sources for gender, all pictures and picture provenance, and all map data: coordinates, display positions, outlines, spatial geometry and basemap assets. Full research notes and unbounded nested source objects are not bundled. A biography URL may still appear when it supports age or residence; it is not labelled or supplied as evidence for gender.

## Reproduce and validate

Run the checks with Python 3.10 or newer; no third-party packages are needed:

```sh
python scripts/validate.py
```

Checks compare paired formats, require 120 unique people per cohort, reconcile party/group totals and source references, recompute regional and locality metrics, reproduce all four ranking lists from the full locality universe, and enforce the flat public schemas. `validation-source-reconciliation.json` also records comparisons against the original reviewed project inputs. `input-provenance.json` stores their SHA-256 hashes without bundling the full research data.

The inspectable exporter can rebuild this repository from the original project's `work/` and `outputs/` inputs:

```sh
python scripts/export.py --source-root /path/to/original-project --output /path/to/export
```

The exporter writes tables and metadata into the output directory; it does not modify the original project. Source documents are linked, not copied.
