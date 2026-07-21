# FABLE-Pakistan — Submission

This is where the final deliverables for the FABLE-Pakistan data pipeline live (SMP 2026,
WIT-LUMS). It's the package meant for the mentor — everything here is a finished output, not
a work-in-progress.

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
- **`FABLE_Pakistan_Trade_Concordance_Final.xlsx`** — the full working version of the
  concordance table, with all the HS-code-level detail.
- **`FABLE_FAOSTAT_Validation.xlsx`** — a sanity check: how our trade numbers compare against
  FAOSTAT's figures for the same years.

### `scripts/` — how to regenerate everything

Each workbook has a matching script that can rebuild it from scratch, no setup required. The
finished file is baked right into the script (as base64), so running it just writes the exact
same `.xlsx` back out — byte for byte, verified with a SHA256 check. No internet connection,
no API keys, no extra packages needed.

To regenerate a file, just run:

```bash
python3 scripts/generate_production_data_standardized.py --output FABLE_Pakistan_Production_Data_Standardized.xlsx
```

Leave off `--output` and it'll save under the original filename automatically.
