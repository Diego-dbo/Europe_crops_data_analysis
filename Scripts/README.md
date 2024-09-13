# Europe Crop Production and Prices Data Analysis

## production_table - Task Log

### Data Preparation

- **Data Collection**  
  **Source:** FAO  
  **Data:** Downloaded data for all crops, Europe region, and 2022 (last available year): [FAO Data](https://www.fao.org/home/search/en/?q=production).

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
  Element AS element,
  Value AS value,
  Unit AS unit,
  
FROM 
  my-portifolio-434417.Europe_Crops.production;
```

- **Convertendo 'value' para FLOAT64**
 ```sql
   CREATE OR REPLACE TABLE `my-portifolio-434417.Europe_Crops.production_cleaned` AS
SELECT 
  country,
  crop,
  element,
  CAST(value AS FLOAT64) AS value,  
  unit
FROM 
  `my-portifolio-434417.Europe_Crops.production_cleaned`;
```




- **Update Values and Units from 100 g/ha to ton/ha in Agricultural**
 ```sql
    UPDATE 
  `my-portifolio-434417.Europe_Crops.production_cleaned`
SET 
  value = ROUND(value * 0.0001, 2),  
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
- **Joining Production and Price Data by Country and Crop**
```SQL
SELECT 
  p.*,                  
  pc.value AS price_value,  
  pc.unit AS price_unit     
FROM 
  `my-portifolio-434417.Europe_Crops.production_cleaned` p
LEFT JOIN 
  `my-portifolio-434417.Europe_Crops.price_cleaned` pc
ON 
  p.country = pc.country AND
  p.crop = pc.crop;
```


  

