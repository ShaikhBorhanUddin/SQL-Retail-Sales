# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `p1_retail_db`

This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `p1_retail_db`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

### 3. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
```csv
|transactions_id|sale_date |sale_time|customer_id|gender|age|category   |quantity|price_per_unit|cogs |total_sale|
|---------------|----------|---------|-----------|------|---|-----------|--------|--------------|-----|----------|
|180            |2022-11-05|10:47:00 |117        |Male  |41 |Clothing   |3       |300           |129  |900       |
|240            |2022-11-05|11:49:00 |95         |Female|23 |Beauty     |1       |300           |123  |300       |
|1256           |2022-11-05|09:58:00 |29         |Male  |23 |Clothing   |2       |500           |190  |1000      |
|1587           |2022-11-05|20:06:00 |140        |Female|40 |Beauty     |4       |300           |105  |1200      |
|1819           |2022-11-05|20:44:00 |83         |Female|35 |Beauty     |2       |50            |13.5 |100       |
|943            |2022-11-05|19:29:00 |90         |Female|57 |Clothing   |4       |300           |318  |1200      |
|1896           |2022-11-05|20:19:00 |87         |Female|30 |Electronics|2       |25            |30.75|50        |
|1137           |2022-11-05|22:34:00 |104        |Male  |46 |Beauty     |2       |500           |145  |1000      |
|856            |2022-11-05|17:43:00 |102        |Male  |54 |Electronics|4       |30            |9.3  |120       |
|214            |2022-11-05|16:31:00 |53         |Male  |20 |Beauty     |2       |30            |8.1  |60        |
|1265           |2022-11-05|14:35:00 |86         |Male  |55 |Clothing   |3       |300           |111  |900       |
```
2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**:
```sql
SELECT 
  *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantity >= 4
```
```csv
|transactions_id|sale_date |sale_time|customer_id|gender|age|category   |quantity|price_per_unit|cogs |total_sale|
|---------------|----------|---------|-----------|------|---|-----------|--------|--------------|-----|----------|
|1484           |2022-11-23|09:29:00 |22         |Female|19 |Clothing   |4       |300           |147  |1200      |
|64             |2022-11-15|06:34:00 |7          |Male  |49 |Clothing   |4       |25            |8.5  |100       |
|284            |2022-11-12|09:17:00 |129        |Male  |43 |Clothing   |4       |50            |20.5 |200       |
|1885           |2022-11-09|07:32:00 |148        |Female|52 |Clothing   |4       |30            |10.8 |120       |
|547            |2022-11-14|07:36:00 |3          |Male  |63 |Clothing   |4       |500           |250  |2000      |
|159            |2022-11-10|21:30:00 |42         |Male  |26 |Clothing   |4       |50            |23.5 |200       |
|699            |2022-11-21|22:21:00 |129        |Female|37 |Clothing   |4       |30            |16.2 |120       |
|1259           |2022-11-03|17:31:00 |105        |Female|45 |Clothing   |4       |50            |21   |200       |
|146            |2022-11-10|22:01:00 |74         |Male  |38 |Clothing   |4       |50            |49   |200       |
|1476           |2022-11-11|22:27:00 |130        |Female|27 |Clothing   |4       |500           |555  |2000      |
|1296           |2022-11-26|20:42:00 |45         |Female|22 |Clothing   |4       |300           |342  |1200      |
|1696           |2022-11-21|17:59:00 |24         |Female|50 |Clothing   |4       |50            |55   |200       |
|1497           |2022-11-19|21:44:00 |109        |Male  |41 |Clothing   |4       |30            |32.4 |120       |
|735            |2022-11-26|21:38:00 |153        |Female|64 |Clothing   |4       |500           |515  |2000      |
|943            |2022-11-05|19:29:00 |90         |Female|57 |Clothing   |4       |300           |318  |1200      |
|965            |2022-11-27|21:45:00 |84         |Male  |22 |Clothing   |4       |50            |13   |200       |
|1615           |2022-11-17|13:43:00 |82         |Female|61 |Clothing   |4       |25            |13.5 |100       |
```

3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
```
```csv
|category       |net_sale  |total_orders|
|---------------|----------|------------|
|Electronics    |311445    |678         |
|Clothing       |309995    |698         |
|Beauty         |286790    |611         |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/1.png)
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/2.png)
4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
```
```csv
|avg_age        |
|---------------|
|40.42          |
```

5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
```
```csv
|transactions_id|sale_date |sale_time|customer_id|gender|age|category   |quantity|price_per_unit|cogs|total_sale|
|---------------|----------|---------|-----------|------|---|-----------|--------|--------------|----|----------|
|522            |2022-07-09|11:00:00 |52         |Male  |46 |Beauty     |3       |500           |145 |1500      |
|559            |2022-12-12|10:48:00 |5          |Female|40 |Clothing   |4       |300           |84  |1200      |
|1522           |2022-11-14|08:35:00 |48         |Male  |46 |Beauty     |3       |500           |235 |1500      |
|1559           |2022-08-20|07:40:00 |49         |Female|40 |Clothing   |4       |300           |144 |1200      |
|421            |2022-04-08|08:43:00 |66         |Female|37 |Clothing   |3       |500           |235 |1500      |
|1421           |2022-01-17|07:07:00 |59         |Female|37 |Clothing   |3       |500           |185 |1500      |
|484            |2022-03-13|07:52:00 |135        |Female|19 |Clothing   |4       |300           |75  |1200      |
|1484           |2022-11-23|09:29:00 |22         |Female|19 |Clothing   |4       |300           |147 |1200      |
|15             |2022-07-01|11:50:00 |75         |Female|42 |Electronics|4       |500           |210 |2000      |
|743            |2022-08-07|07:54:00 |55         |Female|34 |Beauty     |4       |500           |260 |2000      |
|1015           |2022-03-09|11:53:00 |94         |Female|42 |Electronics|4       |500           |200 |2000      |
|1743           |2022-10-26|09:37:00 |47         |Female|34 |Beauty     |4       |500           |250 |2000      |
|742            |2022-03-19|06:08:00 |37         |Female|38 |Electronics|4       |500           |195 |2000      |
|1742           |2022-11-22|08:25:00 |18         |Female|38 |Electronics|4       |500           |220 |2000      |
|420            |2022-01-02|10:53:00 |28         |Female|22 |Clothing   |4       |500           |200 |2000      |
|1420           |2022-04-15|07:01:00 |138        |Female|22 |Clothing   |4       |500           |205 |2000      |
|592            |2022-12-26|09:15:00 |77         |Female|46 |Beauty     |4       |500           |275 |2000      |
|1592           |2022-03-16|09:08:00 |81         |Female|46 |Beauty     |4       |500           |155 |2000      |
|720            |2022-04-08|08:50:00 |116        |Female|56 |Beauty     |3       |500           |235 |1500      |
|1720           |2022-10-10|08:51:00 |28         |Female|56 |Beauty     |3       |500           |190 |1500      |
|269            |2022-09-19|11:31:00 |87         |Male  |25 |Clothing   |4       |500           |250 |2000      |
|320            |2022-04-20|08:35:00 |57         |Female|28 |Electronics|4       |300           |159 |1200      |
|673            |2022-07-04|10:14:00 |18         |Female|43 |Clothing   |3       |500           |270 |1500      |
|1269           |2022-01-01|08:09:00 |71         |Male  |25 |Clothing   |4       |500           |145 |2000      |
|1320           |2022-11-02|11:55:00 |102        |Female|28 |Electronics|4       |300           |84  |1200      |
|1673           |2022-06-14|07:36:00 |42         |Female|43 |Clothing   |3       |500           |185 |1500      |
|142            |2022-04-08|10:05:00 |61         |Male  |35 |Electronics|4       |300           |138 |1200      |
|1142           |2022-11-09|09:49:00 |2          |Male  |35 |Electronics|4       |300           |114 |1200      |
|107            |2022-10-06|09:18:00 |75         |Female|21 |Clothing   |4       |300           |78  |1200      |
|1107           |2022-12-31|11:14:00 |62         |Female|21 |Clothing   |4       |300           |102 |1200      |
|333            |2022-10-06|08:15:00 |21         |Female|54 |Electronics|4       |300           |99  |1200      |
|1333           |2022-11-01|11:38:00 |151        |Female|54 |Electronics|4       |300           |165 |1200      |
|372            |2022-06-19|11:45:00 |27         |Female|24 |Beauty     |3       |500           |140 |1500      |
|1372           |2022-03-18|10:53:00 |60         |Female|24 |Beauty     |3       |500           |145 |1500      |
|54             |2022-10-20|10:17:00 |142        |Female|38 |Electronics|3       |500           |200 |1500      |
|1054           |2022-01-10|09:24:00 |49         |Female|38 |Electronics|3       |500           |140 |1500      |
|193            |2022-03-27|10:40:00 |55         |Male  |35 |Beauty     |3       |500           |180 |1500      |
|577            |2022-04-21|11:55:00 |45         |Male  |21 |Beauty     |4       |500           |215 |2000      |
|1193           |2022-05-11|11:31:00 |50         |Male  |35 |Beauty     |3       |500           |145 |1500      |
|1577           |2022-09-11|06:22:00 |145        |Male  |21 |Beauty     |4       |500           |160 |2000      |
|16             |2022-06-25|10:33:00 |82         |Male  |19 |Clothing   |3       |500           |180 |1500      |
|292            |2022-10-10|06:33:00 |111        |Male  |20 |Beauty     |4       |300           |141 |1200      |
|416            |2022-08-21|09:29:00 |55         |Male  |53 |Electronics|4       |500           |245 |2000      |
|1016           |2022-12-12|07:39:00 |52         |Male  |19 |Clothing   |3       |500           |200 |1500      |
|1292           |2022-05-15|08:20:00 |88         |Male  |20 |Beauty     |4       |300           |90  |1200      |
|1416           |2022-12-29|10:47:00 |111        |Male  |53 |Electronics|4       |500           |125 |2000      |
|257            |2022-12-10|08:49:00 |130        |Male  |19 |Beauty     |4       |500           |165 |2000      |
|1257           |2022-05-10|11:55:00 |29         |Male  |19 |Beauty     |4       |500           |255 |2000      |
|611            |2022-07-21|08:13:00 |11         |Male  |51 |Beauty     |3       |500           |180 |1500      |
|800            |2022-09-19|07:33:00 |111        |Male  |32 |Clothing   |4       |300           |87  |1200      |
|1611           |2022-11-17|07:30:00 |125        |Male  |51 |Beauty     |3       |500           |180 |1500      |
|1800           |2022-08-21|10:53:00 |1          |Male  |32 |Clothing   |4       |300           |111 |1200      |
|506            |2022-04-29|07:13:00 |9          |Male  |34 |Beauty     |3       |500           |200 |1500      |
|1506           |2022-01-09|07:31:00 |52         |Male  |34 |Beauty     |3       |500           |245 |1500      |
|152            |2022-06-16|11:58:00 |120        |Male  |43 |Electronics|4       |500           |210 |2000      |
|1152           |2022-12-26|07:48:00 |87         |Male  |43 |Electronics|4       |500           |170 |2000      |
|547            |2022-11-14|07:36:00 |3          |Male  |63 |Clothing   |4       |500           |250 |2000      |
|1547           |2022-08-11|06:39:00 |142        |Male  |63 |Clothing   |4       |500           |235 |2000      |
|942            |2023-12-01|09:22:00 |35         |Male  |51 |Clothing   |3       |500           |160 |1500      |
|1942           |2023-09-16|11:53:00 |112        |Male  |51 |Clothing   |3       |500           |265 |1500      |
|663            |2023-08-16|06:32:00 |133        |Male  |23 |Clothing   |4       |300           |87  |1200      |
|1663           |2023-12-07|07:04:00 |33         |Male  |23 |Clothing   |4       |300           |81  |1200      |
|313            |2023-12-16|10:03:00 |11         |Female|55 |Beauty     |3       |500           |140 |1500      |
|459            |2023-05-23|07:12:00 |122        |Male  |28 |Clothing   |4       |300           |75  |1200      |
|1313           |2023-06-04|09:22:00 |10         |Female|55 |Beauty     |3       |500           |170 |1500      |
|1459           |2023-11-10|06:46:00 |13         |Male  |28 |Clothing   |4       |300           |144 |1200      |
|636            |2023-05-09|06:15:00 |60         |Female|21 |Beauty     |3       |500           |230 |1500      |
|1636           |2023-07-22|11:26:00 |50         |Female|21 |Beauty     |3       |500           |150 |1500      |
|202            |2023-01-25|06:24:00 |61         |Female|34 |Clothing   |4       |300           |120 |1200      |
|1202           |2023-11-13|06:56:00 |89         |Female|34 |Clothing   |4       |300           |144 |1200      |
|553            |2023-03-20|06:17:00 |106        |Male  |24 |Clothing   |4       |300           |81  |1200      |
|1553           |2023-01-29|08:46:00 |42         |Male  |24 |Clothing   |4       |300           |99  |1200      |
|462            |2023-08-26|10:04:00 |71         |Male  |63 |Electronics|4       |300           |132 |1200      |
|614            |2023-02-13|06:28:00 |61         |Female|39 |Beauty     |4       |300           |120 |1200      |
|808            |2023-11-22|07:18:00 |30         |Male  |33 |Beauty     |4       |500           |195 |2000      |
|1462           |2023-11-13|10:42:00 |124        |Male  |63 |Electronics|4       |300           |114 |1200      |
|1614           |2023-08-23|11:37:00 |135        |Female|39 |Beauty     |4       |300           |105 |1200      |
|1808           |2023-02-12|10:48:00 |109        |Male  |33 |Beauty     |4       |500           |210 |2000      |
|166            |2023-01-28|11:42:00 |32         |Male  |34 |Clothing   |4       |500           |225 |2000      |
|1166           |2023-07-19|07:45:00 |65         |Male  |34 |Clothing   |4       |500           |245 |2000      |
|280            |2023-11-17|09:35:00 |76         |Female|37 |Clothing   |3       |500           |240 |1500      |
|1280           |2023-08-24|09:15:00 |116        |Female|37 |Clothing   |3       |500           |255 |1500      |
|928            |2023-11-05|10:20:00 |54         |Female|35 |Clothing   |4       |300           |90  |1200      |
|1928           |2023-07-29|06:39:00 |93         |Female|35 |Clothing   |4       |300           |75  |1200      |
|332            |2023-04-24|11:28:00 |138        |Male  |58 |Electronics|4       |300           |105 |1200      |
|1332           |2023-12-04|10:02:00 |146        |Male  |58 |Electronics|4       |300           |123 |1200      |
|847            |2023-01-10|08:42:00 |2          |Female|18 |Electronics|4       |300           |162 |1200      |
|1847           |2023-07-28|07:14:00 |5          |Female|18 |Electronics|4       |300           |123 |1200      |
|111            |2023-04-15|09:45:00 |5          |Female|34 |Electronics|3       |500           |130 |1500      |
|1111           |2023-04-30|21:34:00 |2          |Female|34 |Electronics|3       |500           |185 |1500      |
|298            |2023-10-05|19:05:00 |3          |Male  |27 |Beauty     |4       |300           |84  |1200      |
|572            |2023-12-13|18:33:00 |5          |Male  |31 |Clothing   |4       |500           |185 |2000      |
|1298           |2023-05-02|19:51:00 |1          |Male  |27 |Beauty     |4       |300           |120 |1200      |
|1572           |2023-06-18|22:20:00 |1          |Male  |31 |Clothing   |4       |500           |175 |2000      |
|693            |2023-06-08|17:12:00 |1          |Male  |41 |Beauty     |3       |500           |270 |1500      |
|1693           |2023-02-20|18:21:00 |1          |Male  |41 |Beauty     |3       |500           |130 |1500      |
|482            |2023-08-12|18:57:00 |3          |Female|28 |Clothing   |4       |300           |141 |1200      |
|1482           |2023-02-10|22:22:00 |1          |Female|28 |Clothing   |4       |300           |114 |1200      |
|452            |2023-01-30|22:41:00 |4          |Female|48 |Clothing   |3       |500           |240 |1500      |
|946            |2023-08-08|20:15:00 |2          |Male  |62 |Electronics|4       |500           |235 |2000      |
|1452           |2023-08-06|17:41:00 |3          |Female|48 |Clothing   |3       |500           |185 |1500      |
|1946           |2023-07-27|20:48:00 |5          |Male  |62 |Electronics|4       |500           |165 |2000      |
|731            |2023-09-30|18:49:00 |1          |Male  |54 |Clothing   |4       |500           |165 |2000      |
|1731           |2023-12-19|17:41:00 |3          |Male  |54 |Clothing   |4       |500           |195 |2000      |
|164            |2023-02-28|18:26:00 |3          |Female|47 |Beauty     |3       |500           |185 |1500      |
|1164           |2023-04-07|20:53:00 |1          |Female|47 |Beauty     |3       |500           |245 |1500      |
|118            |2023-03-13|20:07:00 |3          |Female|30 |Electronics|4       |500           |270 |2000      |
|970            |2023-05-25|18:13:00 |2          |Male  |59 |Electronics|4       |500           |220 |2000      |
|1118           |2023-10-13|17:24:00 |1          |Female|30 |Electronics|4       |500           |170 |2000      |
|1970           |2023-05-22|17:44:00 |5          |Male  |59 |Electronics|4       |500           |230 |2000      |
|155            |2023-07-18|18:05:00 |3          |Male  |31 |Electronics|4       |500           |150 |2000      |
|1155           |2023-12-03|18:22:00 |3          |Male  |31 |Electronics|4       |500           |255 |2000      |
|647            |2023-03-01|19:53:00 |5          |Male  |59 |Clothing   |3       |500           |190 |1500      |
|1647           |2023-05-01|20:26:00 |5          |Male  |59 |Clothing   |3       |500           |240 |1500      |
|843            |2023-01-25|22:46:00 |3          |Male  |21 |Beauty     |3       |500           |180 |1500      |
|1843           |2023-09-21|18:58:00 |1          |Male  |21 |Beauty     |3       |500           |240 |1500      |
|31             |2023-12-31|17:47:00 |3          |Male  |44 |Electronics|4       |300           |129 |1200      |
|72             |2023-12-06|19:19:00 |5          |Female|20 |Electronics|4       |500           |195 |2000      |
|281            |2023-09-18|20:09:00 |4          |Female|29 |Beauty     |4       |500           |275 |2000      |
|729            |2023-08-26|22:29:00 |3          |Male  |29 |Clothing   |4       |300           |84  |1200      |
|1031           |2023-11-12|21:15:00 |3          |Male  |44 |Electronics|4       |300           |126 |1200      |
|1072           |2023-02-24|18:10:00 |4          |Female|20 |Electronics|4       |500           |180 |2000      |
|1281           |2023-03-14|19:34:00 |4          |Female|29 |Beauty     |4       |500           |165 |2000      |
|1729           |2023-11-22|18:55:00 |82         |Male  |29 |Clothing   |4       |300           |81  |1200      |
|561            |2022-07-29|17:04:00 |34         |Female|64 |Clothing   |4       |500           |250 |2000      |
|1561           |2023-09-17|19:38:00 |16         |Female|64 |Clothing   |4       |500           |170 |2000      |
|67             |2023-08-19|20:19:00 |119        |Female|48 |Beauty     |4       |300           |129 |1200      |
|1067           |2023-10-03|17:01:00 |105        |Female|48 |Beauty     |4       |300           |129 |1200      |
|862            |2022-12-11|21:37:00 |29         |Male  |28 |Electronics|4       |300           |78  |1200      |
|1862           |2022-02-06|22:50:00 |64         |Male  |28 |Electronics|4       |300           |165 |1200      |
|481            |2023-07-13|17:12:00 |48         |Female|43 |Electronics|4       |300           |114 |1200      |
|1481           |2023-11-09|17:22:00 |20         |Female|43 |Electronics|4       |300           |114 |1200      |
|587            |2023-09-04|19:00:00 |91         |Female|40 |Beauty     |4       |300           |99  |1200      |
|1587           |2022-11-05|20:06:00 |140        |Female|40 |Beauty     |4       |300           |105 |1200      |
|212            |2023-10-12|18:13:00 |105        |Male  |21 |Clothing   |3       |500           |215 |1500      |
|1212           |2022-03-16|18:05:00 |142        |Male  |21 |Clothing   |3       |500           |265 |1500      |
|356            |2023-08-27|18:35:00 |71         |Male  |50 |Electronics|3       |500           |255 |1500      |
|1356           |2023-12-18|21:31:00 |11         |Male  |50 |Electronics|3       |500           |245 |1500      |
|726            |2022-06-05|19:37:00 |72         |Male  |47 |Clothing   |4       |300           |126 |1200      |
|1726           |2023-06-26|18:12:00 |13         |Male  |47 |Clothing   |4       |300           |93  |1200      |
|239            |2022-09-19|19:34:00 |1          |Male  |38 |Electronics|3       |500           |165 |1500      |
|669            |2022-01-23|20:24:00 |110        |Male  |24 |Beauty     |4       |300           |87  |1200      |
|1239           |2022-07-08|20:42:00 |134        |Male  |38 |Electronics|3       |500           |255 |1500      |
|1669           |2022-08-04|22:28:00 |83         |Male  |24 |Beauty     |4       |300           |123 |1200      |
|157            |2022-05-15|21:59:00 |98         |Male  |62 |Electronics|4       |500           |170 |2000      |
|839            |2023-11-11|21:02:00 |130        |Female|20 |Electronics|4       |300           |96  |1200      |
|927            |2022-02-21|17:13:00 |83         |Male  |43 |Electronics|4       |500           |250 |2000      |
|1157           |2022-12-23|21:24:00 |81         |Male  |62 |Electronics|4       |500           |270 |2000      |
|1839           |2022-08-28|21:57:00 |92         |Female|20 |Electronics|4       |300           |156 |1200      |
|1927           |2023-09-06|19:44:00 |46         |Male  |43 |Electronics|4       |500           |180 |2000      |
|46             |2022-11-08|17:50:00 |54         |Female|20 |Electronics|4       |300           |84  |1200      |
|1046           |2023-07-21|21:47:00 |5          |Female|20 |Electronics|4       |300           |156 |1200      |
|480            |2022-12-22|22:12:00 |126        |Female|42 |Beauty     |4       |500           |225 |2000      |
|1480           |2023-11-26|18:05:00 |3          |Female|42 |Beauty     |4       |500           |165 |2000      |
|78             |2023-02-17|21:08:00 |68         |Female|47 |Clothing   |3       |500           |265 |1500      |
|1078           |2023-05-04|22:20:00 |16         |Female|47 |Clothing   |3       |500           |125 |1500      |
|447            |2023-04-18|17:57:00 |37         |Male  |22 |Beauty     |4       |500           |245 |2000      |
|1447           |2022-05-30|22:21:00 |137        |Male  |22 |Beauty     |4       |500           |155 |2000      |
|93             |2022-01-25|20:52:00 |148        |Female|35 |Beauty     |4       |500           |140 |2000      |
|1093           |2023-11-06|17:26:00 |87         |Female|35 |Beauty     |4       |500           |270 |2000      |
|144            |2022-03-26|22:18:00 |119        |Female|59 |Beauty     |3       |500           |255 |1500      |
|474            |2022-05-08|17:57:00 |145        |Female|26 |Clothing   |3       |500           |210 |1500      |
|1144           |2022-12-30|21:27:00 |148        |Female|59 |Beauty     |3       |500           |125 |1500      |
|1474           |2022-05-15|20:49:00 |84         |Female|26 |Clothing   |3       |500           |255 |1500      |
|676            |2023-07-10|22:13:00 |80         |Male  |63 |Electronics|3       |500           |205 |1500      |
|1676           |2023-09-21|20:22:00 |91         |Male  |63 |Electronics|3       |500           |210 |1500      |
|773            |2023-01-14|19:10:00 |3          |Male  |25 |Electronics|4       |500           |175 |2000      |
|1773           |2023-12-12|18:50:00 |80         |Male  |25 |Electronics|4       |500           |165 |2000      |
|213            |2023-08-13|20:48:00 |113        |Male  |27 |Beauty     |3       |500           |275 |1500      |
|487            |2023-04-09|21:03:00 |36         |Male  |44 |Clothing   |4       |500           |235 |2000      |
|1213           |2023-06-21|17:23:00 |41         |Male  |27 |Beauty     |3       |500           |185 |1500      |
|1487           |2023-02-01|19:01:00 |131        |Male  |44 |Clothing   |4       |500           |140 |2000      |
|463            |2023-01-29|20:22:00 |55         |Female|54 |Beauty     |3       |500           |175 |1500      |
|1463           |2022-07-29|19:45:00 |98         |Female|54 |Beauty     |3       |500           |170 |1500      |
|13             |2023-02-08|17:43:00 |106        |Male  |22 |Electronics|3       |500           |245 |1500      |
|308            |2022-03-31|19:12:00 |130        |Female|34 |Beauty     |4       |300           |126 |1200      |
|1013           |2022-07-16|19:38:00 |111        |Male  |22 |Electronics|3       |500           |200 |1500      |
|1308           |2023-06-19|22:39:00 |91         |Female|34 |Beauty     |4       |300           |150 |1200      |
|875            |2023-11-30|21:47:00 |134        |Female|51 |Electronics|4       |500           |135 |2000      |
|1875           |2022-06-03|22:42:00 |141        |Female|51 |Electronics|4       |500           |165 |2000      |
|716            |2023-08-13|19:51:00 |137        |Female|60 |Clothing   |4       |300           |108 |1200      |
|1716           |2022-02-12|19:16:00 |39         |Female|60 |Clothing   |4       |300           |87  |1200      |
|648            |2023-02-23|18:13:00 |41         |Male  |53 |Beauty     |4       |300           |138 |1200      |
|1648           |2023-07-10|17:18:00 |16         |Male  |53 |Beauty     |4       |300           |87  |1200      |
|859            |2022-09-20|21:52:00 |46         |Female|56 |Electronics|3       |500           |190 |1500      |
|1859           |2022-09-14|20:58:00 |32         |Female|56 |Electronics|3       |500           |205 |1500      |
|956            |2023-04-24|21:50:00 |140        |Male  |30 |Clothing   |3       |500           |135 |1500      |
|1956           |2023-06-01|20:40:00 |62         |Male  |30 |Clothing   |3       |500           |170 |1500      |
|597            |2022-11-01|19:29:00 |84         |Male  |22 |Beauty     |4       |300           |111 |1200      |
|1597           |2023-08-28|18:21:00 |32         |Male  |22 |Beauty     |4       |300           |78  |1200      |
|368            |2023-01-31|21:11:00 |90         |Female|56 |Clothing   |4       |300           |132 |1200      |
|1368           |2022-03-08|21:29:00 |145        |Female|56 |Clothing   |4       |300           |132 |1200      |
|479            |2022-11-03|21:35:00 |90         |Male  |52 |Electronics|4       |300           |105 |1200      |
|1479           |2022-05-31|22:24:00 |108        |Male  |52 |Electronics|4       |300           |162 |1200      |
|756            |2023-07-17|20:33:00 |4          |Female|62 |Electronics|4       |300           |333 |1200      |
|1756           |2022-05-12|22:16:00 |119        |Female|62 |Electronics|4       |300           |297 |1200      |
|476            |2023-12-12|18:31:00 |131        |Female|27 |Clothing   |4       |500           |570 |2000      |
|1476           |2022-11-11|22:27:00 |130        |Female|27 |Clothing   |4       |500           |555 |2000      |
|253            |2022-09-30|21:26:00 |66         |Female|53 |Clothing   |4       |500           |525 |2000      |
|1253           |2023-12-03|19:58:00 |108        |Female|53 |Clothing   |4       |500           |605 |2000      |
|682            |2023-10-23|20:51:00 |60         |Male  |46 |Beauty     |4       |300           |354 |1200      |
|1682           |2022-12-30|19:30:00 |71         |Male  |46 |Beauty     |4       |300           |315 |1200      |
|296            |2022-12-31|22:44:00 |73         |Female|22 |Clothing   |4       |300           |369 |1200      |
|1296           |2022-11-26|20:42:00 |45         |Female|22 |Clothing   |4       |300           |342 |1200      |
|832            |2022-11-13|17:25:00 |106        |Male  |47 |Beauty     |4       |500           |600 |2000      |
|1832           |2023-11-10|21:17:00 |57         |Male  |47 |Beauty     |4       |500           |480 |2000      |
|165            |2022-09-24|19:01:00 |75         |Female|60 |Clothing   |4       |300           |318 |1200      |
|1165           |2023-12-01|17:04:00 |29         |Female|60 |Clothing   |4       |300           |291 |1200      |
|412            |2022-09-04|19:36:00 |30         |Female|19 |Electronics|4       |500           |570 |2000      |
|1412           |2022-10-13|19:59:00 |75         |Female|19 |Electronics|4       |500           |615 |2000      |
|626            |2022-10-30|21:01:00 |65         |Female|26 |Clothing   |4       |500           |555 |2000      |
|1626           |2022-10-10|19:13:00 |19         |Female|26 |Clothing   |4       |500           |495 |2000      |
|789            |2023-12-06|22:13:00 |34         |Female|61 |Clothing   |4       |500           |510 |2000      |
|1789           |2023-11-10|17:02:00 |144        |Female|61 |Clothing   |4       |500           |615 |2000      |
|89             |2023-12-30|21:15:00 |117        |Female|55 |Electronics|4       |500           |590 |2000      |
|1089           |2023-10-21|18:44:00 |108        |Female|55 |Electronics|4       |500           |555 |2000      |
|524            |2023-09-17|19:52:00 |12         |Male  |46 |Beauty     |4       |300           |297 |1200      |
|1524           |2022-10-26|22:10:00 |115        |Male  |46 |Beauty     |4       |300           |321 |1200      |
|735            |2022-11-26|21:38:00 |153        |Female|64 |Clothing   |4       |500           |515 |2000      |
|1735           |2023-09-05|17:26:00 |86         |Female|64 |Clothing   |4       |500           |505 |2000      |
|385            |2022-11-20|19:06:00 |127        |Male  |50 |Electronics|3       |500           |525 |1500      |
|1385           |2023-11-07|19:22:00 |55         |Male  |50 |Electronics|3       |500           |505 |1500      |
|437            |2023-11-26|18:53:00 |56         |Female|35 |Electronics|4       |300           |345 |1200      |
|1437           |2023-09-04|19:19:00 |76         |Female|35 |Electronics|4       |300           |372 |1200      |
|634            |2022-10-10|19:25:00 |68         |Male  |60 |Electronics|4       |500           |535 |2000      |
|1634           |2023-11-03|17:18:00 |90         |Male  |60 |Electronics|4       |500           |520 |2000      |
|441            |2023-11-06|22:00:00 |85         |Male  |57 |Beauty     |4       |300           |351 |1200      |
|1441           |2023-10-04|21:38:00 |63         |Male  |57 |Beauty     |4       |300           |354 |1200      |
|431            |2022-10-29|22:02:00 |99         |Male  |63 |Electronics|4       |300           |345 |1200      |
|1431           |2023-09-28|21:28:00 |114        |Male  |63 |Electronics|4       |300           |312 |1200      |
|711            |2023-09-23|22:26:00 |103        |Male  |26 |Electronics|3       |500           |575 |1500      |
|943            |2022-11-05|19:29:00 |90         |Female|57 |Clothing   |4       |300           |318 |1200      |
|1711           |2023-09-22|20:33:00 |113        |Male  |26 |Electronics|3       |500           |570 |1500      |
|1943           |2023-11-17|21:00:00 |108        |Female|57 |Clothing   |4       |300           |321 |1200      |
|109            |2023-09-06|19:57:00 |94         |Female|34 |Electronics|4       |500           |560 |2000      |
|1109           |2023-12-13|22:13:00 |114        |Female|34 |Electronics|4       |500           |590 |2000      |
|340            |2023-09-19|22:59:00 |54         |Female|36 |Clothing   |4       |300           |294 |1200      |
|1340           |2023-10-30|20:55:00 |92         |Female|36 |Clothing   |4       |300           |348 |1200      |
|342            |2023-11-05|17:24:00 |85         |Female|43 |Clothing   |4       |500           |500 |2000      |
|1342           |2022-09-18|23:00:00 |114        |Female|43 |Clothing   |4       |500           |485 |2000      |
|503            |2023-10-08|20:06:00 |63         |Male  |45 |Beauty     |4       |500           |570 |2000      |
|869            |2022-09-08|22:16:00 |51         |Male  |37 |Beauty     |3       |500           |485 |1500      |
|1503           |2022-10-17|18:28:00 |67         |Male  |45 |Beauty     |4       |500           |605 |2000      |
|1869           |2022-10-23|19:51:00 |113        |Male  |37 |Beauty     |3       |500           |605 |1500      |
|124            |2022-12-24|21:17:00 |83         |Male  |33 |Clothing   |4       |500           |515 |2000      |
|677            |2022-12-17|21:13:00 |65         |Female|19 |Beauty     |3       |500           |555 |1500      |
|1124           |2023-10-06|20:04:00 |83         |Male  |33 |Clothing   |4       |500           |515 |2000      |
|1677           |2022-10-02|20:51:00 |84         |Female|19 |Beauty     |3       |500           |490 |1500      |
|710            |2022-09-03|21:11:00 |71         |Female|26 |Electronics|3       |500           |495 |1500      |
|1710           |2022-10-23|20:14:00 |104        |Female|26 |Electronics|3       |500           |610 |1500      |
|507            |2022-12-11|21:40:00 |52         |Female|37 |Electronics|3       |500           |485 |1500      |
|1507           |2022-12-27|22:14:00 |95         |Female|37 |Electronics|3       |500           |520 |1500      |
|181            |2023-11-06|19:59:00 |79         |Male  |19 |Electronics|4       |300           |327 |1200      |
|1181           |2022-11-06|18:28:00 |84         |Male  |19 |Electronics|4       |300           |354 |1200      |
|47             |2022-10-22|17:22:00 |96         |Female|40 |Beauty     |3       |500           |600 |1500      |
|405            |2022-10-17|17:55:00 |79         |Female|25 |Clothing   |4       |300           |324 |1200      |
|1047           |2022-12-04|21:53:00 |84         |Female|40 |Beauty     |3       |500           |490 |1500      |
|1405           |2023-10-28|20:08:00 |91         |Female|25 |Clothing   |4       |300           |342 |1200      |
|595            |2022-10-15|21:35:00 |65         |Female|18 |Clothing   |4       |500           |210 |2000      |
|1595           |2023-10-04|17:44:00 |115        |Female|18 |Clothing   |4       |500           |255 |2000      |
|58             |2023-09-16|19:18:00 |53         |Male  |18 |Clothing   |4       |300           |75  |1200      |
|1058           |2022-10-30|18:31:00 |100        |Male  |18 |Clothing   |4       |300           |153 |1200      |
|369            |2023-12-13|19:42:00 |111        |Male  |23 |Electronics|3       |500           |215 |1500      |
|1369           |2022-10-10|21:14:00 |64         |Male  |23 |Electronics|3       |500           |180 |1500      |
|533            |2022-11-13|17:19:00 |92         |Male  |19 |Electronics|3       |500           |155 |1500      |
|1533           |2022-10-29|19:35:00 |67         |Male  |19 |Electronics|3       |500           |255 |1500      |
|169            |2022-11-28|18:47:00 |73         |Male  |18 |Beauty     |3       |500           |145 |1500      |
|1169           |2022-09-25|17:12:00 |101        |Male  |18 |Beauty     |3       |500           |255 |1500      |
|74             |2023-10-05|19:50:00 |56         |Female|18 |Beauty     |4       |500           |205 |2000      |
|1074           |2022-10-04|20:18:00 |67         |Female|18 |Beauty     |4       |500           |230 |2000      |
|424            |2023-12-20|19:21:00 |101        |Male  |57 |Beauty     |4       |300           |147 |1200      |
|1424           |2023-09-05|21:32:00 |54         |Male  |57 |Beauty     |4       |300           |111 |1200      |
|115            |2022-09-02|19:21:00 |67         |Male  |51 |Clothing   |3       |500           |255 |1500      |
|1115           |2023-09-21|17:41:00 |99         |Male  |51 |Clothing   |3       |500           |180 |1500      |
|215            |2022-10-03|21:20:00 |101        |Male  |58 |Clothing   |3       |500           |145 |1500      |
|1215           |2022-11-19|20:44:00 |107        |Male  |58 |Clothing   |3       |500           |130 |1500      |
|112            |2023-12-25|18:44:00 |57         |Male  |37 |Clothing   |3       |500           |165 |1500      |
|608            |2022-12-07|22:19:00 |112        |Female|55 |Electronics|3       |500           |200 |1500      |
|1112           |2022-12-22|17:11:00 |94         |Male  |37 |Clothing   |3       |500           |180 |1500      |
|1608           |2023-09-26|21:01:00 |87         |Female|55 |Electronics|3       |500           |265 |1500      |
|199            |2023-10-26|21:34:00 |53         |Male  |45 |Beauty     |3       |500           |135 |1500      |
|1199           |2023-12-16|17:46:00 |110        |Male  |45 |Beauty     |3       |500           |190 |1500      |
|65             |2022-12-11|20:03:00 |84         |Male  |51 |Electronics|4       |500           |160 |2000      |
|1065           |2023-10-24|15:16:00 |76         |Male  |51 |Electronics|4       |500           |175 |2000      |
|580            |2022-11-14|14:44:00 |104        |Female|31 |Clothing   |3       |500           |200 |1500      |
|1580           |2023-09-21|15:47:00 |105        |Female|31 |Clothing   |3       |500           |250 |1500      |
|700            |2022-09-01|15:07:00 |61         |Male  |36 |Electronics|4       |500           |250 |2000      |
|828            |2022-11-24|15:54:00 |76         |Female|33 |Electronics|4       |300           |132 |1200      |
|1700           |2023-09-27|16:10:00 |87         |Male  |36 |Electronics|4       |500           |210 |2000      |
|1828           |2022-10-14|14:14:00 |99         |Female|33 |Electronics|4       |300           |165 |1200      |
|361            |2022-09-12|16:37:00 |112        |Female|34 |Electronics|4       |300           |81  |1200      |
|1361           |2023-09-12|16:00:00 |89         |Female|34 |Electronics|4       |300           |153 |1200      |
|139            |2023-09-15|14:03:00 |113        |Male  |36 |Beauty     |4       |500           |230 |2000      |
|1139           |2023-12-21|14:23:00 |87         |Male  |36 |Beauty     |4       |500           |230 |2000      |
|99             |2023-11-19|15:12:00 |71         |Female|50 |Electronics|4       |300           |132 |1200      |
|1099           |2022-12-24|12:41:00 |56         |Female|50 |Electronics|4       |300           |162 |1200      |
|757            |2023-10-06|12:10:00 |82         |Female|43 |Electronics|4       |300           |105 |1200      |
|1757           |2023-09-29|16:42:00 |50         |Female|43 |Electronics|4       |300           |132 |1200      |
|664            |2022-09-03|16:52:00 |109        |Female|44 |Clothing   |4       |500           |170 |2000      |
|1664           |2023-12-12|16:44:00 |99         |Female|44 |Clothing   |4       |500           |245 |2000      |
|805            |2022-09-03|13:55:00 |59         |Female|30 |Beauty     |3       |500           |155 |1500      |
|908            |2022-10-30|14:47:00 |64         |Male  |46 |Beauty     |4       |300           |81  |1200      |
|1805           |2023-10-10|13:35:00 |79         |Female|30 |Beauty     |3       |500           |225 |1500      |
|1908           |2023-12-17|12:34:00 |93         |Male  |46 |Beauty     |4       |300           |87  |1200      |
|211            |2022-09-12|14:02:00 |54         |Male  |42 |Beauty     |3       |500           |235 |1500      |
|1211           |2023-11-22|14:59:00 |82         |Male  |42 |Beauty     |3       |500           |235 |1500      |
```
6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    category,
    gender
ORDER BY 1
```
```csv
|category   |gender|total_trans|
|-----------|------|-----------|
|Beauty     |Female|330        |
|Beauty     |Male  |281        |
|Clothing   |Female|347        |
|Clothing   |Male  |351        |
|Electronics|Male  |343        |
|Electronics|Female|335        |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/3.png)

7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**:
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```
```csv
|year|month|avg_sale         |
|----|-----|-----------------|
|2022|7    |541.3414634146342|
|2023|2    |535.531914893617 |
```
8. **Write a SQL query to find the top 5 customers based on the highest total sales **:
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```
```csv
|customer_id|total_sales|
|-----------|-----------|
|3          |38440      |
|1          |30750      |
|5          |30405      |
|2          |25295      |
|4          |23580      |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/4.png)
9. **Write a SQL query to find the number of unique customers who purchased items from each category.**:
```sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
```
```csv
|category   |cnt_unique_cs|
|-----------|-------------|
|Beauty     |141          |
|Clothing   |149          |
|Electronics|144          |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/5.png)
10. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**:
```sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```
```csv
|shift    |total_orders|
|---------|------------|
|Afternoon|377         |
|Evening  |1062        |
|Morning  |548         |
```
11. **Identify customers who haven't made a purchase in the last six months.**:
```sql
WITH recent_purchases AS (
    SELECT DISTINCT customer_id
    FROM retail_sales
    WHERE sale_date >= NOW() - INTERVAL '6 months'
)
SELECT c.customer_id
FROM (SELECT DISTINCT customer_id FROM retail_sales) c
LEFT JOIN recent_purchases rp ON c.customer_id = rp.customer_id
WHERE rp.customer_id IS NULL;
```
```csv
|customer_id|
|-----------|
|87         |
|116        |
|71         |
|68         |
|51         |
|70         |
|146        |
|80         |
|52         |
|132        |
|84         |
|92         |
|101        |
|69         |
|114        |
|115        |
|60         |
|97         |
|108        |
|112        |
|22         |
|59         |
|135        |
|65         |
|127        |
|124        |
|98         |
|149        |
|73         |
|103        |
|11         |
|44         |
|42         |
|121        |
|117        |
|88         |
|82         |
|113        |
|125        |
|119        |
|40         |
|153        |
|43         |
|147        |
|9          |
|120        |
|15         |
|79         |
|26         |
|48         |
|85         |
|72         |
|95         |
|57         |
|19         |
|81         |
|61         |
|77         |
|30         |
|21         |
|131        |
|3          |
|17         |
|28         |
|37         |
|104        |
|5          |
|56         |
|91         |
|151        |
|74         |
|29         |
|54         |
|4          |
|34         |
|138        |
|96         |
|67         |
|83         |
|63         |
|10         |
|90         |
|35         |
|105        |
|45         |
|107        |
|6          |
|134        |
|86         |
|144        |
|39         |
|89         |
|93         |
|36         |
|31         |
|50         |
|102        |
|14         |
|66         |
|109        |
|155        |
|13         |
|118        |
|133        |
|111        |
|2          |
|16         |
|62         |
|75         |
|123        |
|128        |
|126        |
|99         |
|142        |
|152        |
|41         |
|46         |
|53         |
|32         |
|7          |
|100        |
|38         |
|136        |
|150        |
|140        |
|139        |
|12         |
|137        |
|78         |
|24         |
|25         |
|141        |
|122        |
|94         |
|154        |
|49         |
|47         |
|20         |
|33         |
|1          |
|76         |
|106        |
|18         |
|64         |
|110        |
|55         |
|145        |
|148        |
|130        |
|27         |
|129        |
|143        |
|23         |
|58         |
|8          |
```
12. **Identify the highest and least profitable product**
```sql
SELECT category, 
       SUM(total_sale - cogs) AS total_profit
FROM retail_sales
GROUP BY category
ORDER BY total_profit DESC;
```
```csv
|category    |total_profit        |
|------------|--------------------|
|Clothing    |245945.2499999999   |
|Electronics |244767.54999999996  |
|Beauty      |228589.3999999999   |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/7.png)
13. **Identify top 10 Loyal Customers (Highest Repeat Buyers)**
```sql
SELECT customer_id, COUNT(*) AS purchase_count
FROM retail_sales
GROUP BY customer_id
ORDER BY purchase_count DESC
LIMIT 10;
```
```csv
|customer_id|purchase_count|
|-----------|--------------|
|1          |76            |
|3          |76            |
|4          |73            |
|2          |69            |
|5          |63            |
|87         |25            |
|61         |23            |
|85         |22            |
|54         |21            |
|56         |21            |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/8.png)
14. **Calculate revenue contribution by each product category**
```sql
SELECT category, 
       SUM(total_sale) AS category_revenue,
       (SUM(total_sale) / (SELECT SUM(total_sale) FROM retail_sales) * 100) AS revenue_percentage
FROM retail_sales
GROUP BY category
ORDER BY revenue_percentage DESC;
```
```csv
|category      |category_revenue  |revenue_percentage  |
|--------------|------------------|--------------------|
|Electronics   |311445            |34.291423978507645  |
|Clothing      |309995            |34.13177278883102   |
|Beauty        |286790            |31.576803232661334  |
```
![Alt Text](https://github.com/ShaikhBorhanUddin/SQL-Retail-Sales/blob/main/9.png)
## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the SQL scripts provided in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries provided in the `analysis_queries.sql` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

### Stay Updated and Join the Community

For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

- **YouTube**: [Subscribe to my channel for tutorials and insights](https://www.youtube.com/xxxxxxx)
- **Instagram**: [Follow me for daily tips and updates](https://www.instagram.com/xxxxxxxxxxx)
- **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/xxxxxxxxxx)
- **Discord**: [Join our community to learn and grow together](https://discord.gg/xxxxxxxxxx)

Thank you for your support, and I look forward to connecting with you!
