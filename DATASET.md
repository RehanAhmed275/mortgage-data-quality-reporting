# Dataset and reproducibility

Source: CFPB/FFIEC public Home Mortgage Disclosure Act (HMDA) records.

## Download
1. Open https://ffiec.cfpb.gov/data-browser/data/ .
2. Select 2024 and County geography.
3. Choose 12086 — Miami-Dade County, Florida.
4. Leave all institutions selected and optional filters blank.
5. Download the individual-record CSV and name it county_12086.csv.
6. Upload it to /content in Colab. Do not edit the raw file.

The original download interface identified the 2024 One Year dataset.

## Original input fingerprint
- Records: 82,691
- Columns: 99
- Size: 30,928,203 bytes
- SHA-256: `63c28e8e9d82b79472a7da7a80b3332956b5a6fbb33d6f120f59b29bcb6f0e70`

A changed download can produce different counts or byte hashes due to revisions or formatting changes. Preserve the new fingerprint and review scope, rules and findings rather than forcing historical counts. The record-1450 manual note applies only to the original fingerprint.

## Documentation
- https://www.consumerfinance.gov/data-research/hmda/
- https://ffiec.cfpb.gov/data-publication/2024
- https://ffiec.cfpb.gov/documentation/publications/loan-level-datasets/lar-data-fields/

The export uses loan_to_value_ratio as its column name. Consult official definitions before interpreting or reconstructing ratios. Original strings and special values remain preserved throughout the workflow.
