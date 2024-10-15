# Sales Volume

### Verify duplicates for Invoice IDs

```sql

SELECT
	[InvoiceID]
	,COUNT([InvoiceID]) Duplicates
FROM
	[Sales].[Invoices]
GROUP BY 
	[InvoiceID]
HAVING 
	COUNT([InvoiceID]) > 1

```
<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20193820.png "No duplicates for Invoice IDs")

</details>

----------------------------------------------------------

### Total Sales Volume 2013 to 2016

```sql

SELECT
	COUNT([InvoiceID]) AS Sales_Volume_2013_To_2016
FROM
	[Sales].[Invoices]

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot2024-10-02%20181814.png "Total Sales Volume 2013 to 2016")

</details>


-----------------------------------------------------------

### Annual Invoice Volume 2013-2016
```sql
SELECT
	(                             --- 1st Subquery For 2013
	SELECT
		COUNT([InvoiceID])
	FROM
		[Sales].[Invoices]
	WHERE
		[InvoiceDate] BETWEEN '2013-01-10' AND '2013-12-31'
	) AS '2013'
	,
	(                              --- 2nd Subquery For 2014
	SELECT
		COUNT([InvoiceID])
	FROM
		[Sales].[Invoices]
	WHERE
		[InvoiceDate] BETWEEN '2014-01-01' AND '2014-12-31'
	) AS '2014'
	,
	(                               --- 3rd Subquery For 2015
		SELECT
		COUNT([InvoiceID])
	FROM
		[Sales].[Invoices]
	WHERE
		[InvoiceDate] BETWEEN '2015-01-01' AND '2015-12-31'
	) AS '2015'
	,
	(                               --- 4th Subquery For 2016
		SELECT
		COUNT([InvoiceID])
	FROM
		[Sales].[Invoices]
	WHERE
		[InvoiceDate] BETWEEN '2016-01-01' AND '2016-12-31'
	) AS '2016'
```
<details>
<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20182602.png "Annual Invoice Volume 2013-2016")

</details>


