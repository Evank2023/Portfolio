# Data Inspection

#### Data row counts [Sales] schema

Data row counts in the [Sales] schema
- The [InvoiceLines] : **228,265** rows.
- The [Invoices] : **70,510** rows.
- The [OrderLines] : **231,412** rows.
- The [Orders] : **73,595** rows.

```sql
SELECT COUNT(*) AS InvoiceLineNB
FROM [Sales].[InvoiceLines] 

SELECT COUNT(*) AS InvoicesNB
FROM [Sales].[Invoices] 

SELECT COUNT(*) AS OrderLinesNB
FROM [Sales].[OrderLines] 

SELECT COUNT(*) AS OrdersNB
FROM [Sales].[Orders]
```
<details>
	
<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-09-30%20020419.png "Row Count Sales")

</details>

___________________________________________
#### Duplicates in the [Sales] schema

```sql
SELECT [InvoiceLineID] , COUNT(*) AS Count_NB
FROM [Sales].[InvoiceLines]
GROUP BY [InvoiceLineID]
HAVING COUNT(*) >1

SELECT [InvoiceID] , COUNT(*) AS Count_NB
FROM [Sales].[Invoices]
GROUP BY [InvoiceID]
HAVING COUNT(*) >1

SELECT [OrderLineID] , COUNT(*) AS Count_NB
FROM [Sales].[OrderLines]
GROUP BY [OrderLineID]
HAVING COUNT(*) >1

SELECT [OrderID] , COUNT(*) AS Count_NB
FROM [Sales].[Orders]
GROUP BY [OrderID]
HAVING COUNT(*) >1
```

<details>
	
<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/image.png "No duplicates")

</details>

___________________________________________

#### Empty values in the [Sales] schema

```sql
-- Verify Empty Values [Sales].[InvoiceLines]
SELECT 
    [InvoiceLineID]
   ,[InvoiceID]
   ,[Quantity]
   ,[UnitPrice]
FROM 
    [Sales].[InvoiceLines]
WHERE	 
    [InvoiceLineID] IS NULL
 OR [InvoiceID] IS NULL
 OR [Quantity] IS NULL
 OR [UnitPrice] IS NULL
```


```sql
 -- Verify Empty Values [Sales].[Invoices]
SELECT
    [InvoiceID]
   ,[OrderID]
   ,[InvoiceDate]
FROM 
    [Sales].[Invoices]
WHERE	 
    [InvoiceID] IS NULL
 OR [OrderID] IS NULL
 OR [InvoiceDate] IS NULL

```

```sql
-- Verify Empty Values [Sales].[OrderLines]
SELECT
    [OrderLineID]
   ,[OrderID]
   ,[Quantity]
   ,[UnitPrice]
FROM 
    [Sales].[OrderLines]
WHERE
    [OrderLineID] IS NULL
 OR [OrderID] IS NULL
 OR [Quantity] IS NULL
 OR [UnitPrice] IS NULL

```

```sql
 -- Verify Empty Values [Sales].[Orders]
 SELECT 
     [OrderID]
    ,[OrderDate]
 FROM 
     [WideWorldImporters].[Sales].[Orders]
 WHERE 
     [OrderID] IS NULL
 OR  [OrderDate] IS NULL

```
<details>
	
<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/image1.png "No empty values")

</details>

____________________________________________________
















