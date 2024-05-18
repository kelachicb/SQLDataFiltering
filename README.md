# Project Description 
The primary objective of this project is to implement a filtering mechanism targeting Ford Motor Company's stock closing prices across specific days and months within the calendar year. This initiative seeks to enhance data analysis capabilities by selectively filtering and analyzing Ford Motor Company's stock closing prices based on predetermined days and months, facilitating comprehensive market insights.

![Fordpng](https://github.com/kelachicb/SQLDataFiltering/assets/57774879/3a1ef67a-4226-4359-af2a-5b9023c5e2c5)


### Data Extraction
* The data for this project was sourced from the historical price data available on Nasdaq's website. For reference, the data can be accessed directly via the following link: [Nasdaq Historical Price Data for Ford Motor Company](https://www.nasdaq.com/market-activity/stocks/f/historical). Additionally, to facilitate ease of access and analysis, an .xls file containing the relevant data has been provided for your convenience.
  
### Technologies Used
* The initial data file was in .csv format and was opened in Excel for data review and to remove non-relevant columns. The modified file was saved as a .xls format and subsequently imported into Microsoft SQL for query operations and further analysis.
  
## Let's Begin Querying👨🏾‍💻
The initial step in our data analysis journey involved utilizing the `SELECT` statement to retrieve and view all available data fields. This enabled us to comprehensively overview the dataset's structure and content, facilitating subsequent querying and analysis tasks.

```sql
SELECT *
FROM HistoricalData;
```
#### Output:

![image](https://github.com/kelachicb/SQLDataFiltering/assets/57774879/258c533e-ed21-42cd-b7dc-b34544f16054)

Utilizing the `COUNT` function, we determined the number of rows in our dataset.

```sql
SELECT COUNT(*) AS TotalRows
FROM HistoricalData;
```
#### Output:

![image](https://github.com/kelachicb/SQLDataFiltering/assets/57774879/0c032d58-20ba-4cd8-a0bd-b42709f819f6)

## Filtering the Data

**1. Declare a Variable and Create a Table:**

  We initiated the process by creating a variable using the `DECLARE` statement and then using the `INSERT INTO` function to populate this variable with our desired months. After populating our variable with relevant data, we employed the `SELECT` statement with the `WHERE` clause and `DATEPART` function to filter and return the desired days and months from our dataset.
  
```sql
DECLARE @FilteredData TABLE (
    DateValue DATE,
    ClosingPrice DECIMAL(10, 2)
);

INSERT INTO @FilteredData (DateValue, ClosingPrice)
SELECT *
FROM HistoricalData
WHERE 
    (DATEPART(MONTH, Date) IN (3, 6, 9, 12)) -- Months: March, June, September, December
    AND
    (DATEPART(DAY, Date) IN (29, 30, 31));

SELECT *
FROM @FilteredData;
```
#### Output:
![image](https://github.com/kelachicb/SQLDataFiltering/assets/57774879/16c977ff-63a1-48db-8053-17c8aaabb98d)

**2. Count Rows in Filtered Data:**
  
  We utilized the `COUNT()` function to determine the number of rows in our filtered dataset stored in the variable.

```sql
SELECT COUNT(*) AS FilteredRowTotal
FROM @FilteredData;
```
#### Output:

![image](https://github.com/kelachicb/SQLDataFiltering/assets/57774879/86f9a9fa-4973-447e-8e42-26e38f0dcb11)


