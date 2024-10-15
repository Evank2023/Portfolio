# Data Inspection

Data row counts [Sales] schema

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




##### Sales
Total sales for 2013

```sql
SELECT 
	SUM([Invoice_Lines].[Quantity]*[Invoice_Lines].[UnitPrice]) AS Total_Sales_2013

FROM 
	[Sales].[Invoices] AS Invoices,
	[Sales].[InvoiceLines] AS Invoice_Lines

WHERE 
	[Invoices].[InvoiceID] = [Invoice_Lines].[InvoiceID]
	AND
	[InvoiceDate] BETWEEN '2013-01-01' AND '2013-12-31'
```
Daily total sales for January 2013
```sql
