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

## OR Between filter - Date
### To calculate the average of column `15 year rate` in table `Interest Rates` between August 1 or August 2
```
Average 15 year rate btwn AUG 1 or 2 = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]=DATE(2018,8,1) || 'Interest Rates'[Date]=DATE(2018,8,2))
```

## Range of values or Threshold filters with AND
### To calculate the average of column `15 year rate` in table `Interest Rates` between in August 
```
Average 15 year rate for AUG = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),'Interest Rates'[Date]>=DATE(2018,8,1) && 'Interest Rates'[Date]<=DATE(2018,8,31))
```

## ALL function 
### Simply saying apply this value to all members of a column or a table at large
### Given one data to all members of a column or a full table 
```
Average interest rate to all dates = CALCULATE(AVERAGE('Interest Rates'[15 year rate]),ALL('Interest Rates'[Date]))
```

## FILTER function 
### FILTER("table","filter condition")
### the filter function returns the calculate of the specific conditions mentioned. 
## When to use the FILTER Function
  * Column = measure
  * Column = formula
  * Column = column
  * Measure = measure
  * Measure = formula
  * Measure = fixed value

  * can also be `<>`,`>`,`<`,`>=`,`=<!`
```
August 1 =  DATE(2018,8,1)
```
#### Column = measure
```
Interest rate August 1 (filter example) = CALCULATE(AVERAGE('Interest Rates'[15 year rate]), FILTER('Interest Rates', 'Interest Rates'[Date] = [August 1]))
```


## GENERATESERIES function - DATA POPULATION
### GENERATESERIES("start value","end value","interval")
```
loan Period (table_name) = GENERATESERIES(1,360,1)
```
