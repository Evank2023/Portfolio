# Minimum date and Maximum date for Invoice and Order

```sql
--- Invoice ---
SELECT
	 MIN(InvoiceDate) AS Min_Date
	,MAX(InvoiceDate) AS Max_Date
FROM
	[Sales].[Invoices]

```

<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20194528.png " Invoice Min 
& Max Date ")

</details>


```sql
--- Order ---
SELECT
	 MIN(OrderDate) AS Min_Date
	,MAX(OrderDate) AS Max_Date
FROM
	[Sales].[Orders]
```
<details>

<summary>Result Screenshot</summary>

![alt text]( https://github.com/Evank2023/Portfolio/blob/WWI/ResultScreenshot/Screenshot%202024-10-02%20194547.png " Order Min & Max Date ")

</details>
