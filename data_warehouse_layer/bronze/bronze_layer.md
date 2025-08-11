## Bronze Layer Pipeline Overview
The diagram represents a pipeline in **Azure Data Factory (ADF)** for the Bronze Layer with the following workflow:

![ADF Staging to Bronze](img_bronze/PL_staging_2_Bronze.png)

1. **Lookup1**
   - Performs a **Lookup** activity to query the configuration table.
   - Retrieves parameters in the **source** such as `container`, `path`, and `file`.
   - Retrieves the target **sink** details such as table name and schema name.
   - Passes these results to the **ForEach** activity.

2. **ForEach1**
   - Iterates through each item from the **Lookup1** output.
   - Contains two sub-activities:
     - **Copy data1**: Copies data from the **Staging Layer** (files) into the **Bronze Layer** (tables).
       - All columns are stored as `NVARCHAR(MAX)` to avoid data load failures caused by mismatched or incompatible data types.
     - **Pipeline_Failed_Alert**: Triggered when **Copy data1** fails, sending an alert/notification.
     - **Fail2**: Executes if **Copy data1** fails, marking the error for that specific iteration.

3. **Fail2**
   - Executes if the **ForEach** activity fails completely or encounters a critical error.
   - Stops the pipeline and logs the failure.

### Workflow Summary

‘Lookup1 → ForEach1 → (Copy data1 → On failure: Pipeline_Failed_Alert on Fail1) → If ForEach fails → Fail2’

![ADF Staging to Bronze](img_bronze/Bronze_Layer.png)