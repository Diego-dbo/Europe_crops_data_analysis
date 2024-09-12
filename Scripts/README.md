# Europe Crop Production and Prices Data Analysis

## production_table - Task Log

### Data Preparation

- **Data Collection**  
  **Source:** FAO  
  **Data:** Downloaded data for all crops, Europe region, and 2022 (last available year): [FAO Data](https://www.fao.org).

### Data Processing

- **Formatted and standardized headers**  
  The data headers were standardized using Microsoft Excel.

- **Data Cleaning and Transformation using SQL and BigQuery**

- **Created a new table (`production_cleaned`), selected useful columns, and renamed them**
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

- **Conversion of measurement units from 100 grams per hectare (100 g/ha) to tons per hectare (ton/ha)**
    ```sql
    UPDATE 
      `my-portifolio-434417.Europe_Crops.production_cleaned`
    SET 
      value = value * 0.0001
    WHERE 
      unit = '100 g/ha';
    ```

- **Updated the column `unit` from '100 g/ha' to 'ton/ha'**
    ```sql
    UPDATE 
      `my-portifolio-434417.Europe_Crops.production_cleaned`
    SET 
      unit = 'ton/ha'
    WHERE 
      unit = '100 g/ha';
    ```
## price_table - Task Log

### Data Preparation

- **Data Collection**  
  **Source:** FAO  
  **Data:** Downloaded data for all crops, Europe region, and 2022 (last available year): [FAO Data](https://www.fao.org).

### Data Processing

- **Formatted and standardized headers**  
  The data headers were standardized using Microsoft Excel.

- **Data Cleaning and Transformation using SQL and BigQuery**
  
- **Created a new table (`price_cleaned`), selected useful columns, and renamed them**
 ```sql
  CREATE OR REPLACE TABLE my-portifolio-434417.Europe_Crops.price_cleaned AS
SELECT 
  Area AS country, 
  Item AS crop, 
  Unit AS unit, 
  Value AS value
FROM 
  my-portifolio-434417.Europe_Crops.price;
```
- **Updated  column `unit` from 'USD' to 'USD/tonne'**
```sql
  UPDATE 
  `my-portifolio-434417.Europe_Crops.price_cleaned`
SET 
  unit = 'USD/tonne'
WHERE 
  unit = 'USD';
```


  

