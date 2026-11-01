# Data dictionary

`member_id` uniquely identifies a person within an election cohort. Join each year's source files to that year's member file using `member_id`; `name_he` is included for readability. Join locality populations through `cbs_locality_code` and the correct population reference year. The 2026 cohort uses the 2024 population files.

All CSV rows are flat. Empty cells mean missing or not applicable. Dates use ISO `YYYY-MM-DD` when a full date is available; a year-only value must be interpreted with the date-precision column. Multiple locality claims recorded for one source are separated by ` | `.

| Column | Meaning |
| --- | --- |
| `age` | Exact age or inclusive age range, using an en dash; blank when unknown. |
| `age_basis` | birth_date, birth_year, reported_age or not_available; identifies the factual basis of the age. |
| `age_reference_date` | Date on which the age value is measured. |
| `age_source_url` | Primary birth-date, birth-year or reported-age source. |
| `analysis_subdistrict_he` | Subdistrict grouping for comparisons; Judea and Samaria is one group. |
| `birth_date` | Full birth date when available. |
| `birth_year` | Birth year when stated by the cited source; blank when only a range is known. |
| `birth_year_max` | Latest birth year supported by a reported-age range; blank when unnecessary or unknown. |
| `birth_year_min` | Earliest birth year supported by a reported-age range; blank when unnecessary or unknown. |
| `bloc` | Political grouping: Bibi Bloc, Ultra Orthodox, Arab Parties or Change Bloc. |
| `cbs_locality_code` | CBS statistical-locality code; blank for unmatched places. |
| `claim_type` | birth_date, birth_year or reported_age. Blank where the source claim type is not separately recorded. |
| `coalition_group` | Coalition/Opposition grouping, with the distinct 2022 and 2026 definitions in the README. |
| `date_precision` | Recorded precision of the source publication date. |
| `district_code` | CBS district code. |
| `district_he` | District classification in Hebrew. |
| `election_date` | Election date. |
| `election_year` | Election/cohort year, 2022 or 2026. |
| `electoral_list_he` | List at the election; the joint Religious Zionism/Otzma/Noam list is one list in 2022. |
| `gender` | Male/Female category. Gender sources are not included. |
| `geography_reference_year` | Reference year of the administrative classifications. |
| `geography_source_url` | Primary source for administrative classifications. |
| `knesset` | Knesset number, 25 or 26. |
| `list_rank` | Position on the electoral list. |
| `locality_he` | Assigned residence locality in member files; CBS statistical locality in population files. |
| `locality_original_he` | Unnormalized place name in the original December 2022 research table. |
| `member_id` | Member identifier within the election cohort. |
| `municipal_status_code` | Original CBS municipal-status code; distinct from municipality-type code. |
| `municipal_status_he` | Original CBS municipal-status label. |
| `municipality_code` | CBS municipality/council code, when present in the input. |
| `municipality_he` | Administrative municipality or council; may contain several named places. |
| `municipality_reference_year` | Reference year for the municipality type, when separately recorded. |
| `municipality_type_code` | CBS municipality type: 1 city, 2 local council, 3 regional council, 4 no municipal status. |
| `municipality_type_he` | Municipality/council type in Hebrew. |
| `name_he` | Hebrew public name. |
| `party_component_he` | Component party within an electoral list, when available. |
| `party_he` | Party or electoral-list label used for the member. |
| `population` | Persons in the specified CBS population column; blank means unavailable, not zero. |
| `population_reference_date` | End-of-year population reference date. |
| `population_reference_year` | Population year, 2022 or 2024. |
| `population_source_column_he` | Exact Hebrew CBS input-column name used for population. |
| `publication_date` | Publication date of the source, when known. |
| `reference_year` | Reference year of a classification source. |
| `reported_age` | Age stated by a dated publication, which may differ from age on the cohort reference date. |
| `reported_age_date` | Publication date of the reported-age evidence. |
| `reported_locality_he` | Locality explicitly recorded for that residence source; it can differ from the assigned locality. |
| `residence_reference_date` | Reference date of the residence table, distinct from the date of an individual source. |
| `residence_source_date` | Primary residence-source publication date; for 2022, the historical table reference date. |
| `residence_source_date_precision` | Recorded precision of the residence-source date, such as day or year. |
| `residence_source_url` | Primary residence source. The relative historical CSV reference resolves within this repository. |
| `source_role` | primary, supporting or additional; relative to the subject of that source table. |
| `source_url` | Public source URL, or the included historical CSV filename. |
| `subdistrict_code` | CBS subdistrict code. |
| `subdistrict_he` | Recorded administrative subdistrict classification in Hebrew. |
| `unit_he` | National, district or subdistrict name in Hebrew. |
| `unit_type` | national, district or subdistrict. Each population-region file has 1, 7 and 16 rows respectively. |
