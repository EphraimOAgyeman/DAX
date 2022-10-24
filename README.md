<img src="bi.webp" align="center" size="1000px"/>

# DAX

Data Analysis Expressions

### Parts of DAX 
>`name given to expression` = `CALCULATE` ( `FUNCTION_NAME`(`TABLE_NAME`[`COLUMN_NAME`]), `FILTER`)

---
## Average function
### To calculate the average of column `15 year rate` in table `Interest Rates`
```
Average 15 year rate = CALCULATE(AVERAGE('Interest Rates'[15 year rate]))
```

## Date filter
### To calculate the average of column `15 year rate` in table `Interest Rates` in August
```
Average 15 year rate for AUG = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]=DATE(2018,8,1))
```

## Not filter - Date
### To calculate the average of column `15 year rate` in table `Interest Rates` not in August
```
Average 15 year rate not for AUG = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]<>DATE(2018,8,1))
```

## And or Between filter - Date
### To calculate the average of column `15 year rate` in table `Interest Rates` between August 1 and August 2
```
Average 15 year rate btwn AUG 1 and 2 = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]=DATE(2018,8,1),'Interest Rates'[Date]=DATE(2018,8,2))
```

