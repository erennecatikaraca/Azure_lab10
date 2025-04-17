# Azure_lab10
# Azure Synapse Product Data Pipeline

This project demonstrates a simple Azure Synapse Analytics data integration pipeline. It loads product data from a CSV file in Azure Data Lake Storage Gen2 into a dedicated SQL pool table, with logic to insert new products and update existing ones based on a surrogate key.

## Overview

The pipeline performs the following steps:

1. **Reads product data** from a `Product.csv` file stored in Azure Data Lake Storage Gen2.
2. **Looks up existing products** in the `dbo.DimProduct` table by matching `ProductID` with `ProductAltKey`.
3. **Inserts new records** where no match is found.
4. **Updates existing records** where a match is found.
5. **Loads the final data** into a dedicated SQL pool using a Synapse Data Flow.

## Technologies Used

- Azure Synapse Analytics
- Azure Data Lake Storage Gen2
- Synapse Pipelines & Data Flows
- Dedicated SQL Pool (formerly SQL DW)

## Data Sources

- **Input:** `files/data/Product.csv`
- **Destination Table:** `dbo.DimProduct`

## Data Flow Steps

- **Source:** Read CSV file from Data Lake
- **Source:** Read existing products from SQL table
- **Lookup:** Match products by `ProductID`
- **Alter Row:** Determine insert or upsert action
- **Sink:** Write to `dbo.DimProduct` table

## How to Run

1. Deploy resources via Azure portal.
2. Open Synapse Studio.
3. Configure and publish the data pipeline.
4. Enable debug mode to test the data flow.
5. Run the pipeline manually or via trigger.
6. Verify results in the `dbo.DimProduct` table.

## Notes

- Uses **System Assigned Managed Identity** for secure authentication.
- Handles **schema drift** for flexible data handling.
- Type 1 Slowly Changing Dimension logic via `Alter Row`.
