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

_________________________________________

### Invoice Volume ASC vs DESC

```sql

--- Invoice Volume 2013 ---

WITH MonthlyVolume AS (
SELECT 
	YEAR([Sales].[Invoices].[InvoiceDate]) AS Year,
	MONTH([Sales].[Invoices].[InvoiceDate]) AS Month,
    COUNT(CASE WHEN YEAR([InvoiceDate]) = 2013 THEN [InvoiceID] END) AS Invoice_Volume
FROM 
    [Sales].[Invoices]
WHERE 
    [InvoiceDate] BETWEEN '2013-01-01' AND '2013-12-31'  
GROUP BY 
    YEAR([Sales].[Invoices].[InvoiceDate]),
	MONTH([Sales].[Invoices].[InvoiceDate])
)

SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.Invoice_Volume AS Invoice_Volume_Asc, 
    B.Month AS MonthDesc, 
    B.Invoice_Volume AS Invoice_Volume_Desc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume ASC) AS RowAsc FROM MonthlyVolume) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume DESC) AS RowDesc FROM MonthlyVolume) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.Invoice_Volume ASC

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-17%20222727.png " Invoice Volume ")

</details>

___________________________________________________________

```sql

--- Invoice Volume 2014 ---

WITH MonthlyVolume AS (
SELECT 
	YEAR([Sales].[Invoices].[InvoiceDate]) AS Year,
	MONTH([Sales].[Invoices].[InvoiceDate]) AS Month,
    COUNT(CASE WHEN YEAR([InvoiceDate]) = 2014 THEN [InvoiceID] END) AS Invoice_Volume
FROM 
    [Sales].[Invoices]
WHERE 
    [InvoiceDate] BETWEEN '2014-01-01' AND '2014-12-31'  
GROUP BY 
    YEAR([Sales].[Invoices].[InvoiceDate]),
	MONTH([Sales].[Invoices].[InvoiceDate])
)

SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.Invoice_Volume AS Invoice_Volume_Asc, 
    B.Month AS MonthDesc, 
    B.Invoice_Volume AS Invoice_Volume_Desc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume ASC) AS RowAsc FROM MonthlyVolume) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume DESC) AS RowDesc FROM MonthlyVolume) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.Invoice_Volume ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-17%20224531.png " Invoice Volume 2014 ")

</details>

______________________________________________________________

```sql
--- Invoice Volume 2015 ---

WITH MonthlyVolume AS (
SELECT 
	YEAR([Sales].[Invoices].[InvoiceDate]) AS Year,
	MONTH([Sales].[Invoices].[InvoiceDate]) AS Month,
    COUNT(CASE WHEN YEAR([InvoiceDate]) = 2015 THEN [InvoiceID] END) AS Invoice_Volume
FROM 
    [Sales].[Invoices]
WHERE 
    [InvoiceDate] BETWEEN '2015-01-01' AND '2015-12-31'  
GROUP BY 
    YEAR([Sales].[Invoices].[InvoiceDate]),
	MONTH([Sales].[Invoices].[InvoiceDate])
)

SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.Invoice_Volume AS Invoice_Volume_Asc, 
    B.Month AS MonthDesc, 
    B.Invoice_Volume AS Invoice_Volume_Desc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume ASC) AS RowAsc FROM MonthlyVolume) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume DESC) AS RowDesc FROM MonthlyVolume) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.Invoice_Volume ASC
```


<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-17%20225020.png " Invoice Volume 2015 ")

</details>

____________________________________________________

```sql

--- Invoice Volume 2016 ---

WITH MonthlyVolume AS (
SELECT 
	YEAR([Sales].[Invoices].[InvoiceDate]) AS Year,
	MONTH([Sales].[Invoices].[InvoiceDate]) AS Month,
    COUNT(CASE WHEN YEAR([InvoiceDate]) = 2016 THEN [InvoiceID] END) AS Invoice_Volume
FROM 
    [Sales].[Invoices]
WHERE 
    [InvoiceDate] BETWEEN '2016-01-01' AND '2016-05-31'  
GROUP BY 
    YEAR([Sales].[Invoices].[InvoiceDate]),
	MONTH([Sales].[Invoices].[InvoiceDate])
)

SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.Invoice_Volume AS Invoice_Volume_Asc, 
    B.Month AS MonthDesc, 
    B.Invoice_Volume AS Invoice_Volume_Desc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume ASC) AS RowAsc FROM MonthlyVolume) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY Invoice_Volume DESC) AS RowDesc FROM MonthlyVolume) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.Invoice_Volume ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-17%20225404.png " Invoice Volyme 2016 ")

</details>























