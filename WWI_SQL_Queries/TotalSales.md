# Annual Total Sales & Monthly Total Sales
Regarding the sales amount, we can refer to the **[Sales].[Invoices]** and **[Sales].[InvoiceLines]** tables. 
The **[Sales].[InvoiceLines]** table contains the details of invoices such as quantity and unit price, 
while the **[Sales].[Invoices]** table contains the invoice date. These tables are joinable using the Invoice ID.

_________________________________________________________________________

### Total Sales 2013 to 2015

```sql
SELECT 
    SUM(CASE 
            WHEN InvoiceDate BETWEEN '2013-01-01' AND '2013-12-31' 
            THEN Invoice_Lines.Quantity * Invoice_Lines.UnitPrice 
            ELSE 0 
        END) AS Total_Sales_2013,
    SUM(CASE 
            WHEN InvoiceDate BETWEEN '2014-01-01' AND '2014-12-31' 
            THEN Invoice_Lines.Quantity * Invoice_Lines.UnitPrice 
            ELSE 0 
        END) AS Total_Sales_2014,
    SUM(CASE 
            WHEN InvoiceDate BETWEEN '2015-01-01' AND '2015-12-31' 
            THEN Invoice_Lines.Quantity * Invoice_Lines.UnitPrice 
            ELSE 0 
        END) AS Total_Sales_2015
FROM 
    [Sales].[Invoices] AS Invoices
JOIN 
    [Sales].[InvoiceLines] AS Invoice_Lines 
    ON Invoices.InvoiceID = Invoice_Lines.InvoiceID
WHERE 
    InvoiceDate BETWEEN '2013-01-01' AND '2015-12-31'
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20071247.png " Total Sales 2013 to 2015 ")

</details>

> [!Note]
> The `CASE` statement allows to calculate the sales amount for different date ranges within a single `SUM()` operation.
_________________________________________________________
### Total Monthly Sales

```sql
SELECT 
  FORMAT(InvoiceDate, 'MM') AS Month,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2013 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2013,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2014 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2014,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2015 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2015,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2016 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2016
FROM 
    [Sales].[Invoices] AS Invoices
JOIN 
    [Sales].[InvoiceLines] AS Invoice_Lines
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
> `FORMAT(InvoiceDate, 'MM')` is used to extract the month part from the date without the year.
The `CASE` statements check the year of the InvoiceDate and calculate the total sales for each specific year (2013, 2014, 2015).
The `GROUP BY` and `ORDER BY` clauses will automatically sort by year and month because of the `FORMAT(InvoiceDate, 'yyyy-MM')`.

_________________________________________________________________

### Total Daily Sales

```sql
SELECT 
  FORMAT(InvoiceDate, 'MM-dd') AS Date,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2013 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2013,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2014 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2014,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2015 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2015,
  SUM(CASE WHEN YEAR(InvoiceDate) = 2016 THEN Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice] ELSE 0 END) AS Sales_2016
FROM 
    [Sales].[Invoices] AS Invoices
JOIN 
    [Sales].[InvoiceLines] AS Invoice_Lines
ON 
    Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
WHERE 
    InvoiceDate BETWEEN '2013-01-01' AND '2016-05-31'
GROUP BY 
    FORMAT(InvoiceDate, 'MM-dd')
ORDER BY 
    Date


```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20075415.png " Daily Sales 2013 to 2016 ")

</details>

_____________________________________________________________________

### Order By VS DESC

```sql
--- 2013 Sales ---
WITH MonthlySales AS (
    SELECT 
        YEAR(Invoices.[InvoiceDate]) AS Year, 
        MONTH(Invoices.[InvoiceDate]) AS Month,
        SUM(Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice]) AS MonthlySales
    FROM 
        [Sales].[Invoices] AS Invoices
    JOIN 
        [Sales].[InvoiceLines] AS Invoice_Lines
        ON Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
    WHERE 
        Invoices.[InvoiceDate] BETWEEN '2013-01-01' AND '2013-12-31'
    GROUP BY 
        YEAR(Invoices.[InvoiceDate]), 
        MONTH(Invoices.[InvoiceDate])
)

-- Applying separate ranks to force ascending and descending sales
SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.MonthlySales AS MonthlySalesAsc, 
    B.Month AS MonthDesc, 
    B.MonthlySales AS MonthlySalesDesc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales ASC) AS RowAsc FROM MonthlySales) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales DESC) AS RowDesc FROM MonthlySales) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.MonthlySales ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20081827.png " 2013 ")

</details>



```sql
--- 2014 Sales ---
WITH MonthlySales AS (
    SELECT 
        YEAR(Invoices.[InvoiceDate]) AS Year, 
        MONTH(Invoices.[InvoiceDate]) AS Month,
        SUM(Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice]) AS MonthlySales
    FROM 
        [Sales].[Invoices] AS Invoices
    JOIN 
        [Sales].[InvoiceLines] AS Invoice_Lines
        ON Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
    WHERE 
        Invoices.[InvoiceDate] BETWEEN '2014-01-01' AND '2014-12-31'
    GROUP BY 
        YEAR(Invoices.[InvoiceDate]), 
        MONTH(Invoices.[InvoiceDate])
)

-- Applying separate ranks to force ascending and descending sales
SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.MonthlySales AS MonthlySalesAsc, 
    B.Month AS MonthDesc, 
    B.MonthlySales AS MonthlySalesDesc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales ASC) AS RowAsc FROM MonthlySales) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales DESC) AS RowDesc FROM MonthlySales) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.MonthlySales ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20082822.png " 2014 ")

</details>



```sql
--- 2015 Sales ---
WITH MonthlySales AS (
    SELECT 
        YEAR(Invoices.[InvoiceDate]) AS Year, 
        MONTH(Invoices.[InvoiceDate]) AS Month,
        SUM(Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice]) AS MonthlySales
    FROM 
        [Sales].[Invoices] AS Invoices
    JOIN 
        [Sales].[InvoiceLines] AS Invoice_Lines
        ON Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
    WHERE 
        Invoices.[InvoiceDate] BETWEEN '2015-01-01' AND '2015-12-31'
    GROUP BY 
        YEAR(Invoices.[InvoiceDate]), 
        MONTH(Invoices.[InvoiceDate])
)

-- Applying separate ranks to force ascending and descending sales
SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.MonthlySales AS MonthlySalesAsc, 
    B.Month AS MonthDesc, 
    B.MonthlySales AS MonthlySalesDesc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales ASC) AS RowAsc FROM MonthlySales) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales DESC) AS RowDesc FROM MonthlySales) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.MonthlySales ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20083113.png " 2015 ")

</details>



```sql
--- 2016 Sales ---
WITH MonthlySales AS (
    SELECT 
        YEAR(Invoices.[InvoiceDate]) AS Year, 
        MONTH(Invoices.[InvoiceDate]) AS Month,
        SUM(Invoice_Lines.[Quantity] * Invoice_Lines.[UnitPrice]) AS MonthlySales
    FROM 
        [Sales].[Invoices] AS Invoices
    JOIN 
        [Sales].[InvoiceLines] AS Invoice_Lines
        ON Invoices.[InvoiceID] = Invoice_Lines.[InvoiceID]
    WHERE 
        Invoices.[InvoiceDate] BETWEEN '2016-01-01' AND '2016-05-31'
    GROUP BY 
        YEAR(Invoices.[InvoiceDate]), 
        MONTH(Invoices.[InvoiceDate])
)

-- Applying separate ranks to force ascending and descending sales
SELECT 
    A.Year, 
    A.Month AS MonthAsc, 
    A.MonthlySales AS MonthlySalesAsc, 
    B.Month AS MonthDesc, 
    B.MonthlySales AS MonthlySalesDesc
FROM 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales ASC) AS RowAsc FROM MonthlySales) A
JOIN 
    (SELECT *, ROW_NUMBER() OVER (ORDER BY MonthlySales DESC) AS RowDesc FROM MonthlySales) B
    ON A.RowAsc = B.RowDesc
ORDER BY 
    A.MonthlySales ASC
```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-16%20083426.png " 2016 ")

</details>

> [!NOTE]
> **Common Table Expression (CTE)** :
> 
> - The `MonthlySales` CTE calculates the total sales for each month in year by summing the products of quantity and unit price from the `InvoiceLines`.
> 
> **Row Numbering** :
> 
> - The first subquery (aliased as `A`) calculates `ROW_NUMBER()` for the monthly sales in ascending order.
> - The second subquery (aliased as `B`) calculates `ROW_NUMBER()` for the same monthly sales in descending order.
> 
> **Joining** :
> 
> - The two subqueries are joined based on the row numbers (`RowAsc` and `RowDesc`) to align the results of ascending and descending sales on the same row.
> 
> **Selecting Columns** :
> 
> - The final selection includes both months (`MonthAsc` and `MonthDesc`) and their corresponding sales figures (`MonthlySalesAsc` and `MonthlySalesDesc`).
> 
> **Ordering** :
> 
> - The final result is ordered by `MonthlySalesAsc`, but you can adjust this ordering as needed.
> 
> **Output:**
> 
> - This query will provide a side-by-side comparison of the monthly sales figures in ascending and descending order, allowing for easy analysis.











