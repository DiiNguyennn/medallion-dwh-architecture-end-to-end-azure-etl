## Azure Data Factory Pipeline Overview

The diagram represents a pipeline in **Azure Data Factory (ADF)** with the following workflow:

![ADF Source to Staging](landing_zone/img_staging/data_staging.png)

1. **Lookup1**
   - Executes a **Lookup** activity to query a configuration table.
   - Retrieves parameters  in both **source** and**sink** such as `container`, `path`, and `file`.
   - Passes the results to the **ForEach** activity.

2. **ForEach1**
   - Iterates over each item from the **Lookup1** output.
   - Contains two sub-activities:
     - **Copy data1**: Transfers data from the source system to the staging area.
     - **Pipeline_Failed_Alert**: Triggered when **Copy data1** fails, sending an alert/notification.
     - **Fail2**: Executes if **Copy data1** fails, marking the error for that specific iteration.

3. **Fail1**
   - Runs if the **ForEach** activity fails entirely or encounters a critical error.
   - Stops the pipeline and logs the failure.

### Workflow Summary

`Lookup1 → ForEach1 → (Copy data1 → On failure: Pipeline_Failed_Alert on Fail2) → If ForEach fails → Fail1`

![Data in Staging (ADLS Gen 2)](landing_zone/img_staging/pl_source_2_staging.png)
