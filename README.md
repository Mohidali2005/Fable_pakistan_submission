# FABLE-Pakistan — Submission

Deliverable files for the FABLE-Pakistan data pipeline (SMP 2026, WIT-LUMS), for submission to the mentor.

## Structure

- **`excel_files/`** — the 7 deliverable workbooks:
  - `FABLE_Pakistan_Production_Data_Standardized.xlsx` — Deliverable #1, provincial crop/livestock production (42 commodity sheets, 2000-01 to 2024-25)
  - `FABLE_Pakistan_Trade_Data.xlsx` — raw UN Comtrade pull, one sheet per HS code, both flows, 2000-2025
  - `FABLE_Trade_Aggregated.xlsx` — HS codes rolled up into FABLE-commodity trade totals
  - `FABLE_Trade_Production_Joined.xlsx` — Deliverable #2, the national production+trade balance table
  - `FABLE_Pakistan_Concordance.xlsx` — Deliverable #3, the FABLE-Pakistan concordance table
  - `FABLE_FAOSTAT_Validation.xlsx` — our trade figures validated against FAOSTAT
  - `FABLE_Pakistan_Trade_Concordance_Final.xlsx` — the full working HS-code trade concordance table

- **`scripts/`** — one reproducibility script per workbook above. Each script has zero external
  dependencies (only the Python standard library): the finished `.xlsx` is embedded inside the
  script as a base64 blob and is written out byte-for-byte identical every time it's run. Verified
  via SHA256 match against the file in `excel_files/` at generation time.

  ```bash
  python3 scripts/generate_production_data_standardized.py --output FABLE_Pakistan_Production_Data_Standardized.xlsx
  ```

  (Each script defaults `--output` to the original filename if omitted.)
