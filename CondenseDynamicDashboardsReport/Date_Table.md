
#### Data Dimension Table

```c
Dim_Date = 
ADDCOLUMNS(
    CALENDAR("2022-01-01", "2024-12-31"),
    "DateInt", FORMAT([Date], "YYYYMMDD"),
    "Year", YEAR([Date]),
    "MonthNumber", MONTH([Date]),
    "MonthNameShort", FORMAT([Date], "MMM"),
    "MonthNameLong", FORMAT([Date], "MMMM"),
    "DayOfWeekNumber", WEEKDAY([Date]),
    "DayOfWeek", FORMAT([Date], "dddd"),
    "DayOfWeekShort", FORMAT([Date], "ddd"),
    "Quarter", "Q" & FORMAT([Date], "Q"),
    "YearQuarter", FORMAT([Date], "YYYY") & "/Q" & FORMAT([Date], "Q"),
    "EndOfMonth", EOMONTH([Date], 0)
)
```

#### Calculated Column "Inpast"

```c
Inpast = 
VAR MaxDate = MAX(Fact_Sales[Date])
VAR PriorYear = EDATE(MaxDate, -12)
RETURN
    Dim_Date[Date] <= PriorYear
```
