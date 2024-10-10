#### These measures allow selecting and displaying values via a slicer.

```c
Select_YTD = 
VAR selected_value = SELECTEDVALUE(Select_Values[Values])
VAR result = SWITCH(selected_value,
    "Sales Amount", [YTD_Sales_SW],
    "Sales Volume", [YTD_Quantity_SW],
    "Gross Profit", [YTD_Gross_Profit_SW],
    BLANK()
)
RETURN
result
```


```c
Select_PYTD = 
VAR selected_value = SELECTEDVALUE(Select_Values[Values])
VAR result = SWITCH(selected_value,
    "Sales Amount", [PYTD_Gross_Profit_SW],
    "Sales Volume", [PYTD_Quantity_SW],
    "Gross Profit", [PYTD_Gross_Profit_SW],
    BLANK()
)
RETURN
result
```
