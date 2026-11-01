# Knesset members: residence and demographic data

Raw tables for the original 120 elected members of the 25th and 26th Knessets, with population inputs for geographic comparisons.

[Yoav Fried](https://yoavfried.com) · [Knesset on the Map](https://yoavfried.com/knesset-map)

| Election | Residence reference | Age reference | Population reference |
| --- | --- | --- | --- |
| 2022 — 25th Knesset | 28 December 2022 | 1 November 2022 | 31 December 2022 |
| 2026 — 26th Knesset | 1 November 2026 | 1 November 2026 | 31 December 2024 |

Each cohort contains the original 120 elected members, without later replacements. The 2026 roster follows completed-count reporting available on 1 November 2026. The 2022 roster source is [the elected-members list published on 4 November 2022](https://www.inn.co.il/news/581997). The 2026 roster sources are [ynet](https://www.ynet.co.il/news/article/sk0nhz11afl) and [i24NEWS](https://www.i24news.tv/he/news/israel-elections-2026/artc-12604d2f).

## Files

| File | Contents |
| --- | --- |
| `members-2022.csv`, `members-2026.csv` | Member facts, locality and administrative classifications, electoral list/component, political grouping, gender, birth date/year, age or age range, and primary residence/age sources |
| `residence-sources-2022.csv`, `residence-sources-2026.csv` | Residence sources, recorded locality claims and source dates |
| `age-sources-2022.csv`, `age-sources-2026.csv` | Birth-date, birth-year and reported-age sources |
| `classification-sources-2022.csv`, `classification-sources-2026.csv` | Sources for administrative classifications |
| `historical-residences-2022.csv` | Original December 2022 residence table, preserving original locality spellings |
| `population-localities-2022.csv`, `population-localities-2024.csv` | Complete CBS locality inputs: 1,484 and 1,490 rows, including places with no MK and places without a published population |
| `population-regions-2022.csv`, `population-regions-2024.csv` | Published national, district and subdistrict population inputs |

All files are UTF-8 CSV with English column names. Hebrew names end in `_he`. Empty cells mean unknown, unavailable or not applicable; they do not mean zero. Source URLs are included in the corresponding rows. The [data dictionary](DATA_DICTIONARY.md) defines every column and join key.

## Reading the data

The 2022 residence assignments come from the original December 2022 research table. That table did not record separate citations for every residence. Its original place names are preserved in `historical-residences-2022.csv`; member records use normalized names. Current residence evidence is not backdated to 2022. Residence source dates describe the evidence, which may predate the cohort reference date. Additional sources can describe older or alternative localities; the assigned locality is in the member table.

2022 electoral-list labels reflect the election: Religious Zionism, Otzma Yehudit and Noam were one 14-member list, with component parties recorded separately. `coalition_group` in 2022 groups the 64 members of the incoming coalition. In 2026 it groups the outgoing five-party camp: Likud, Religious Zionism, Otzma Yehudit, Shas and United Torah Judaism; it is a political grouping rather than a claim about formal coalition membership on the reference date.

Age is measured on 1 November of each election year. A full birth date yields an exact age; a birth year yields a range. Missing ages remain blank. Itamar Eitam's reported age establishes a 1980–1981 birth-year range without an exact birth year. Abd al-Karim Masri's 1964 birth year is stated by one secondary biographical page. Four 2026 members have no age established in these sources.

Population covers all ages using the CBS population column identified in each locality row. The 2024 analysis column covers Israelis and excludes the separately published foreign-national column. Judea and Samaria population covers Israeli localities only. The entire area forms one `analysis_subdistrict_he` group. Canonical 2022 administrative labels use the 2024 CBS reference; their district/subdistrict assignments agree with the 2022 locality file. Historical municipality type is retained where it changed.

The national denominators are 9,662,000 for 2022 and 9,805,100 for 2024. Regional figures are published to 0.1 thousand: the 2022 regional sum is 100 above the national total, and rounded district/subdistrict subtotals can differ. Do not replace the national denominator with the locality-file sum, which omits residents outside localities. Locality population refers to the complete CBS statistical locality; some named places share a municipality. Pnei Kedem and Jewish Hebron lack separate comparable official populations in both cohorts; Yishuv HaDaat also lacks one for 2026. Their member records are retained.

This repository contains table data only. It excludes pictures, picture sources, gender sources and spatial map data. A biography URL can appear as an age or residence source.
