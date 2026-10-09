# Mortgage Data Quality & Reporting

**Rehan Ahmed · Python · SQL · SQLite · Excel**

A tested portfolio workflow that processes **82,691 public mortgage records**, preserves source values, records validation exceptions and produces reconciled reports.

[Open in Google Colab](https://colab.research.google.com/github/RehanAhmed275/mortgage-data-quality-reporting/blob/main/Mortgage_Data_Analysis.ipynb) · [Read the explained notebook](Mortgage_Data_Analysis.ipynb) · [Download the example Excel report](reports/Mortgage_Data_Quality_Report_2024.xlsx) · [Get the dataset](DATASET.md)

## Business problem
Mortgage reporting needs consistent records, explicit definitions and traceable quality checks. This project demonstrates how an analyst can retain ambiguous records, distinguish warnings from technical failures, and reconcile source counts with analytical outputs.

This is an independent public-data project, not Pegasus internal data or an underwriting decision system.

## Results
| Measure | Result |
|---|---:|
| Source records / fields | 82,691 / 99 |
| Lender identifiers | 737 |
| Validation rules | 16 |
| Records with review warnings | 1,544 (1.87%) |
| Warning events | 1,646 |
| Quarantined records | 0 |
| Isolated test cases passed | 22 |
| Originations | 33,869 |
| Lenders with originations | 610 |

Warning events overlap. They are review candidates, not confirmed defects. Zero quarantined records means no failures under the implemented ERROR rules.

## Workflow
1. Load raw CSV strings without collapsing blank, NA and Exempt values.
2. Profile fields and preserve the file fingerprint and source-record number.
3. Parse numeric fields and retain DTI ranges independently.
4. Evaluate 11 ERROR rules and 5 WARNING rules; retain traceable exception events.
5. Test altered records in isolation, plus duplicate-group and overlapping-warning scenarios.
6. Load a transactional SQLite snapshot with keys, indexes and reporting views. Verify repeatable loading.
7. Reconcile SQL reports against pandas summaries.
8. Export eight CSV reports, a nine-sheet Excel workbook and a verified working backup.

## Findings
- Site-built 1–4-unit properties account for 33,689 originations and USD 15.904 billion in summed reported amounts.
- Multifamily site-built properties account for 128 originations and USD 2.060 billion: approximately 0.38% of originations but 11.46% of reported amount.
- Separate property segments improve interpretation of average loan amounts and lender rankings.
- 219 repeated occurrences belong to 415 exact-match-group records. These were retained because identical public rows do not establish duplicate applications.

## Run in Google Colab
1. Use the Open in Google Colab link above, or download the notebook and upload it to Colab.
2. Follow DATASET.md and upload county_12086.csv into /content.
3. Run the notebook's 48 code cells in order. Markdown explains each step.
4. If dependencies are missing, install them with `%pip install -r requirements.txt` after uploading requirements.txt to Colab, then restart the runtime if needed.
5. Download the outputs from the final cell and save the notebook separately.

The code targets Colab. A local Jupyter run requires adapting /content paths and replacing the final google.colab download calls. Dependency ranges are compatibility guidance, not an exact environment lock. SQLite is included in Python.

## Repository contents
| File | Purpose |
|---|---|
| Mortgage_Data_Analysis.ipynb | Explained workflow, tests and saved results |
| reports/Mortgage_Data_Quality_Report_2024.xlsx | Verified example report |
| requirements.txt | Third-party dependencies |
| DATASET.md | Download instructions and fingerprint |
| .gitignore | Excludes raw CSV, generated databases and backup archives |

The full raw dataset, generated SQLite database and backup ZIP are intentionally excluded. They are reproduced by running the notebook.

## Verification
The core pipeline and SQL reporting were independently rerun with local path substitutions and display calls omitted. Exported report tables were compared with recalculated values. The updated notebook contains successful workbook/backup verification outputs. Chart titles and snapshot-specific notes were subsequently corrected.

## Limitations
- US HMDA data for one county and year; not Canadian underwriting or live business operations.
- Public values are privacy-modified. Reported sums are not audited transaction totals.
- Validation covers selected structural/parsing checks, not full conditional HMDA compliance or numeric plausibility.
- Loan-to-value 727.68 on source record 1450 of the original fingerprint in DATASET.md is a documented manual review candidate outside the automated warning count.
- Exact DTI values exist only for a subset; ranges are not imputed to midpoints.
- Database reruns replace one snapshot; no history, scheduler or production monitoring is implemented.
- Headers and release descriptions are configured for this source. Review them before changing scope.
- Reporting outputs are static snapshots. A PASS label is not a mortgage approval or a guarantee of complete correctness.
