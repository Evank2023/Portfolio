#### Year to Date measures

```c
YTD_Gross_Profit_SW = TOTALYTD([Gross_Profit_SW],Fact_Sales[Date])
```

```c
YTD_Quantity_SW = TOTALYTD([Sum_Quantity_SW],Fact_Sales[Date])
```

```c
YTD_Sales_SW = TOTALYTD([Sum_Sales_SW], Fact_Sales[Date])
```

#### Prior Year to Date Measures


```c
PYTD_Gross_Profit_SW = 
CALCULATE(
    [Gross_Profit_SW], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]),
    Dim_Date[Inpast] = TRUE
)
```


```c
PYTD_Quantity_SW = 
CALCULATE(
    [Sum_Quantity_SW], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]),
    Dim_Date[Inpast] = TRUE
)
```


```c
PYTD_Sales_SW = 
CALCULATE(
    [Sum_Sales_SW], 
    SAMEPERIODLASTYEAR(Dim_Date[Date]),
    Dim_Date[Inpast] = TRUE
)
```
