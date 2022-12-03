<img src="bi.webp" align="center" size="1000px"/>

# DAX CHEATSHEET
## **NB:** The sure way to know the right DAX to use and actually apply, is to totally understand what to achieve and how in psuedo code.

Data Analysis Expressions

Dax is used to create or write measures.

There is a difference between calculated columns and measures. In writing measure, avoid using names of columns but rater only measures. Whilst writing calculated columns, you are to use only column names.

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

## POWER function 
### POWER("base","exponent") ie 2^3 - 2 will be the base and 3 the exponent
```
power(1 + [1. Annual interest rate (30 year loan)],1/12)
```

## DIVIDE function 
### DIVIDE("numerator","denominator","alternate results") 
### The divide function returns a value which is defined. If the value isnt returned or is undefined, the alternate results we will provide will show
```
DIVIDE("measure","measure",0)
```

## X-Factor functions 
### Examples of such functions includes `SUMX`,`COUNTX`,`PRODUCTX`,`MAXX`,`MINXX`
### Each will iterate throught the measure table to give the result

```
#SUMX Function
measure = SUMX("table/column","measure or expression")
```

### The main question is, what two data filters do you want to sum up. 

Two question; 1. what is your target data or first data, 2. what other data results you want to add up
### If you want to sum a specific part in a column, we will apply filters in the first parameter of the SUMX function


## Quick Mearures
### Examples of such functions includes 
* `Aggregate per category`
* `Filters`
* `Time intelligence`
* `Totals`
* `Mathematical operations`
* `Text`

### Each will iterate throught the measure table to give the result


## Creating a date table or column
### DATE(year, month, day)
### GENERATESERIES( start value, end value, interval)

```
GENERATESERIES(DATE(start year, start month, start day), DATE(end year, end month, end date))
```


## Filtering among tables
There must be a relationship created before multiTable filtering can be done. The code below is used for such relationship building.
```
 SELECTEDVALUE(column)
```
### GENERATESERIES( start value, end value, interval)

```
GENERATESERIES(DATE(start year, start month, start day), DATE(end year, end month, end date))
```

## IF condition 
### IF(condition 1 is met, "Result", "Alternate result")
```
 IF(MONTH([Date Interest rate selected])<12, DATE(YEAR(Date Interest rate selected), MONTH(Date Interest rate selected)+1,1), DATE(YEAR(Date Interest rate selected)+1,1,1)
```

## Dynamic Measures
### IF the condition is met, we return the first measure and if not, the alternative measure
SELECTEDVALUE(data source) = "text"
```
 IF(condition meets criteria, "measure 1", "measure 2")
```

## DATEIFF Measure function
### it calculates the difference between two dates in units of interval we specify. ie month, day, year etc..
## Both `start date` and `end date` must be measures.
```
DATEIFF(start date, end date, interval)
```

## BlANK Function
### BLANK() = 0, shows up as a " "

example
DIVIDE(numerator, denominator, BLANK())

## Variables in DAX
### Variables work similarly to measures, declare the name and write the purpose or function
### The variable must start the DAX code
```
VAR acurracyFormula = POWER(base values, exponent value )

return accuracyFormula -+ anyother measure
```

```
sample measure =
VAR sampleVAR = plenty

return sampleVAR -+ anything including ifs or filters or other measures
```

# DATE functions
```
dimDate =
ADDCOLUMNS{
   CALENDER(
      DATE(2018, 1, 1),
      DATE(2022, 12, 31)
   ),
   "Year", YEAR([Date]),
   "Quarter", QUARTER([Date]),
   "Quater label", "Q" & QUATER([Date]),
   "Month", MONTH([Date]),
   "Month label", FORMAT([Date]), "mmm"
}
```





## DATESBETWEEN function
### A sleek way of calculating the difference between two dates 
## Both `start date` and `end date` must be measures.
### The date column has to be filtered
### One can use `SUMX` on filtered dates
```
DATESBETWEEN(dates column, start date, end date)
```
```
measure name = SUMX(DATESBETWEEN(dates column, start date, end date), column to sum up)
```


## DATEADD function as a filter
### It is not a stand alone function and its used to move a date column 
```
DATEADD(dates column, number of units or intervals to move by, unit or lenght of interval)
```

## DATESQTD and DATESYTD function as a filter
### Quater-to-date and year-to-date functions
### They have special intervals for date calculations. QTD - in quaters, YTD - in years
```
DATESQTD(date column)
DATESYTD(date column)
```


## Design principles
* F pattern
* A few colors or a color palette [here](https://color.adobe.com/create/color-wheel)
