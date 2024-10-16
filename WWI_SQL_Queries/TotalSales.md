# Annual Total Sales & Monthly Total Sales
Regarding the sales amount, we can refer to the [Sales].[Invoices] and [Sales].[InvoiceLines] tables. 
The [Sales].[InvoiceLines] table contains the details of invoices such as quantity and unit price, 
while the [Sales].[Invoices] table contains the invoice date. These tables are joinable using the Invoice ID.

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













