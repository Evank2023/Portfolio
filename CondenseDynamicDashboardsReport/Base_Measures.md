#### Measure to calculate Gross Profit Margin as a percentage
```c
%_Gross_Profit_SW = DIVIDE([Gross_Profit_SW],[Sum_Sales_SW])
```

#### Measure to calculate Gross Profit
```c
Gross_Profit_SW = [Sum_Sales_SW] - [Sum_Cost_SW]
```

#### Sum of Cost of Goods Sold (COGS)
```c
Sum_Cost_SW = SUM(Fact_Sales[Total_Cost])
```

#### Sum of Quantity (Sold Unit)
```c
Sum_Quantity_SW = SUM(Fact_Sales[Total_Quantity])
```

#### Sum of Sales (Revenue)
```c
Sum_Sales_SW = SUM(Fact_Sales[Total_Sales])
```
