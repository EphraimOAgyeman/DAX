<img src="bi.webp" align="center" size="1000px"/>

# DAX

Data Analysis Expressions

### Parts of DAX 
>`name given to expression` = `CALCULATE` ( `FUNCTION_NAME`(`TABLE_NAME`[`COLUMN_NAME`]), `FILTER`)


To calculate the average of column `15 year rate` in table `Interest Rates`
```
Average 15 year rate = CALCULATE(AVERAGE('Interest Rates'[15 year rate]))
```

To calculate the average of column `15 year rate` in table `Interest Rates` in August
```
Average 15 year rate for AUG = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]=DATE(2018,8,1))
```

To calculate the average of column `15 year rate` in table `Interest Rates` not in August
```
Average 15 year rate not for AUG = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]<>DATE(2018,8,1))
```
