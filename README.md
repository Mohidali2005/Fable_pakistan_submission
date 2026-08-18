# FABLE-Pakistan — Submission

This is where the final deliverables for the FABLE-Pakistan data pipeline live (SMP 2026,
WIT-LUMS).

## What's in here

### `excel_files/` — the 7 Excel workbooks

- **`FABLE_Pakistan_Production_Data_Standardized.xlsx`** (Deliverable #1) — how much of each
  crop and livestock product Pakistan produced, broken down by province, from 2000-01 to
  2024-25. 42 sheets, one per commodity.
- **`FABLE_Trade_Production_Joined.xlsx`** (Deliverable #2) — the main event: production,
  imports, and exports side by side for every FABLE commodity, so you can see the full national
  balance for each one.
- **`FABLE_Pakistan_Concordance.xlsx`** (Deliverable #3) — the table that maps Pakistani crop
  names to their FAO/HS trade codes. This is what makes the other files possible to build.
- **`FABLE_Pakistan_Trade_Data.xlsx`** — the raw trade data pulled from UN Comtrade, before any
  processing — one sheet per HS code, imports and exports, 2000-2025.
- **`FABLE_Trade_Aggregated.xlsx`** — the same trade data, but rolled up from individual HS
  codes into totals per FABLE commodity.
- **`FABLE_Trade_FiveYear_Averages.xlsx`** — trade data as 5-year averages (2000-2005,
  2005-2010, ... 2020-2025) instead of annual figures, since FABLE itself runs in 5-year
  steps. One sheet per FABLE commodity, each with separate Export and Import tables.
- **`FABLE_Pakistan_Trade_Concordance_Final.xlsx`** — the full working version of the
  concordance table, with all the HS-code-level detail.
- **`FABLE_FAOSTAT_Validation.xlsx`** — a sanity check: how our trade numbers compare against
  FAOSTAT's figures for the same years.

### `excel_scripts/` — how to regenerate everything

Each workbook has a matching script that can rebuild it from scratch, no setup required. The
finished file is baked right into the script (as base64), so running it just writes the exact
same `.xlsx` back out — byte for byte, verified with a SHA256 check. No internet connection,
no API keys, no extra packages needed.

To regenerate a file, just run:

```bash
python3 excel_scripts/generate_production_data_standardized.py --output FABLE_Pakistan_Production_Data_Standardized.xlsx
```

Leave off `--output` and it'll save under the original filename automatically.

### `csvs/` — the flat-file versions

The same underlying data as `excel_files/`, but as plain CSVs where a flat table makes more sense
than a multi-sheet workbook:

- **`FABLE_Pakistan_Concordance.csv`** (Deliverable #3) — the CSV form of the concordance table.
- **`FABLE_Pakistan_Production_Standardized.csv`** (Deliverable #1) — all 42 production
  commodities combined into one flat table.
- **`FABLE_Trade_Production_Joined.csv`** (Deliverable #2) — the national production/trade
  balance table.
- **`FABLE_Trade_Aggregated.csv`** — trade rolled up into FABLE-commodity totals.
- **`FABLE_Trade_FiveYear_Averages.csv`** — the flat-table version of the 5-year-average trade
  data, one row per commodity per 5-year window per flow (Export/Import).
- **`FABLE_Pakistan_Trade_Raw.csv`** — the raw Comtrade pull, one row per HS code, year, and flow.

### `csv_scripts/` — how to regenerate the CSVs

Same idea as `excel_scripts/`: one script per CSV in `csvs/`, each with the finished file baked in as
base64, verified byte-for-byte with SHA256, no dependencies beyond the Python standard library.

```bash
python3 csv_scripts/generate_concordance_csv.py --output FABLE_Pakistan_Concordance.csv
```

### `report/` — the write-up

- **`FABLE_Pakistan_Project_Report.pdf`** — the project report: what was built, how, and what
  the results show.
- **`FABLE_Pakistan_Decisions_Log.pdf`** — the full technical decision log behind the report,
  covering every unit conversion, tariff-code fix, and conversion-factor source, with reasoning
  and citations for each.
