# Annual Total Sales & Monthly Total Sales
Regarding the sales amount, we can refer to the **[Sales].[Invoices]** and **[Sales].[InvoiceLines]** tables. 
The **[Sales].[InvoiceLines]** table contains the details of invoices such as quantity and unit price, 
while the **[Sales].[Invoices]** table contains the invoice date. These tables are joinable using the Invoice ID.

_________________________________________________________________________

#### Total Sales 2013 to 2015

```sql
SELECT (
SELECT 
	SUM(Invoice_Lines.[Quantity]*Invoice_Lines.[UnitPrice])

FROM 
	[WideWorldImporters].[Sales].[Invoices] AS Invoices,
	[WideWorldImporters].[Sales].[InvoiceLines] AS Invoice_Lines

WHERE 
	Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID] and
	InvoiceDate between '2013-01-01' and '2013-12-31'
	) as Total_Sales_2013
	,
	(
SELECT 
	SUM(Invoice_Lines.[Quantity]*Invoice_Lines.[UnitPrice])

FROM 
	[WideWorldImporters].[Sales].[Invoices] AS Invoices,
	[WideWorldImporters].[Sales].[InvoiceLines] AS Invoice_Lines

WHERE 
	Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID] and
	InvoiceDate between '2014-01-01' and '2014-01-31'
	) as Total_Sales_2014
	,
	(
SELECT 
	SUM(Invoice_Lines.[Quantity]*Invoice_Lines.[UnitPrice])

FROM 
	[WideWorldImporters].[Sales].[Invoices] AS Invoices,
	[WideWorldImporters].[Sales].[InvoiceLines] AS Invoice_Lines

WHERE 
	Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID] and
	InvoiceDate between '2015-01-01' and '2015-01-31'
	) as Total_Sales_2015

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20071247.png " Total Sales 2013 to 2015 ")

</details>

_________________________________________________________
#### Total Monthly Sales

```sql
SELECT 
  FORMAT(InvoiceDate, 'MM') AS Month,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2013 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2013,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2014 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2014,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2015 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2015,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2016 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2016
FROM 
    [WideWorldImporters].[Sales].[Invoices] AS Invoices
JOIN 
    [WideWorldImporters].[Sales].[InvoiceLines] AS Invoice_Lines
ON 
    Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
WHERE 
    InvoiceDate BETWEEN '2013-01-01' AND '2016-05-31'
GROUP BY 
    FORMAT(InvoiceDate, 'MM')
ORDER BY 
    Month

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20072931.png " Monthly Sales ")

</details>

> [!NOTE]
> **FORMAT(InvoiceDate, 'MM')** is used to extract the month part from the date without the year.
The **CASE** statements check the year of the InvoiceDate and calculate the total sales for each specific year (2013, 2014, 2015).
The **GROUP BY** and **ORDER BY** clauses will automatically sort by year and month because of the **FORMAT(InvoiceDate, 'yyyy-MM')**.










