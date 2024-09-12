# Europe Crop Production and Prices Data Analysis

## Production_table - Task Log

### Data Preparation

- **Data Collection**  
  **Source:** FAO  
  **Data:** Downloaded data for all crops, Europe region, and 2022 (last available year): [FAO Data](https://www.fao.org).

### Data Processing

- **Formatted and standardized headers**  
  The data headers were standardized using Microsoft Excel.

- **Data Cleaning and Transformation using SQL and BigQuery**

  - **Created a new table, selected useful columns, and renamed them**  
    ```sql
    CREATE OR REPLACE TABLE my-portifolio-434417.Europe_Crops.production_cleaned AS
    SELECT 
      Area AS country, 
      Item AS crop, 
      Unit AS unit,
      Value AS value
    FROM 
      my-portifolio-434417.Europe_Crops.production;
    ```



  
