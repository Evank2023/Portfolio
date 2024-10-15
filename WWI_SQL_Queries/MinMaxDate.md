# Find the start date and end date for Invoices and Orders

```sql

SELECT
	 MIN(InvoiceDate) AS Min_Date
	,MAX(InvoiceDate) AS Max_Date
FROM
	[Sales].[Invoices]

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20194528.png " Invoices Date ")

</details>


```sql
SELECT
	 MIN(OrderDate) AS Min_Date
	,MAX(OrderDate) AS Max_Date
FROM
	[Sales].[Orders]
```
<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20194547.png " Orders Date ")

</details>
