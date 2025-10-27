# Hospital Data Ingestion

This notebook orchestrates the ingestion of hospital datasets, managing both metadata and bronze schemas. The metadata schema tracks information about hospital related tables, while the bronze layer stores raw tables loaded from API-downloaded files.

The notebook performs three main functions:

1. **Parallel Dataset Download:** Hospital dataset files are downloaded in parallel and saved as Delta tables if they are new or if their modified date is more recent than the one recorded in the metadata table.

2. **Metadata Table Update:** The `hospital_metadata` table is updated by inserting new records for previously untracked tables or updating columns such as `last_updated_date` and `batch_date` to reflect the latest data load.

3. **Bronze Table Load:** Bronze tables are loaded in parallel from the Delta files. After loading, the run flag is reset to 'N' to indicate the table has been processed.