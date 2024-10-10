#### These dynamic titles refer to the Select_YTD and Select_PYTD measures and dynamically change part of the title.

#### Header title
```c
Report_Title = "Plant Co. " & SELECTEDVALUE(Select_Values[Values]) & " Performance " & SELECTEDVALUE(Dim_Date[Year])
```

#### Walterfall chart
```c
Waterfall_Title = SELECTEDVALUE(Select_Values[Values]) & " Growth Per Month -> Country -> Product Type"
```

#### Tree Map Chart
```c
Treemap_Title = "10 Bottom Countries | " & SELECTEDVALUE(Select_Values[Values]) & " Growth"
```


#### Column Chart
```c
Column_Chart_Title = SELECTEDVALUE(Select_Values[Values]) & " Growth Per Month"
```


#### Scatter Chart
```c
Scatter_Title = "Account Profitability Segmentation | Gross Profit % and " & SELECTEDVALUE(Select_Values[Values])
```
