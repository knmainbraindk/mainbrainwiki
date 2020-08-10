---
title: "Sharepoint Online Calculated Field Formulas"
zid: "KB-200729161307"
tags:
- sharepoint
- field
---

# Calculated Field Formulas

* 10/20/2016
* 15 minutes to read

_**Applies to:** SharePoint Foundation 2010_

The following tables provide information about the various kinds of formulas you can implement in a calculated field by using the [Formula](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ms461927(v=office.14)) of the [Microsoft.SharePoint.SPFieldCalculated](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ms415687(v=office.14)) class.

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#important-notes)Important Notes

Note

Microsoft SharePoint Foundation formulas for calculated fields are based on Microsoft Excel functions and syntax. However, Microsoft supports only those functions mentioned on this page for use in SharePoint Foundation calculated fields. For example, the Excel function MID is not supported.

Important

All example formulas in this topic use commas "," as the parameter delimiter character. In some countries, the comma is reserved for use as the decimal mark. In such countries, users creating a calculated field must use semi-colons ";" as the delimiter character. Regardless of which character is used when the field is created, the formula works on lists in SharePoint websites anywhere in the world. SharePoint automatically changes the delimiter character to the one that is appropriate for the language/culture of the current page. For example, suppose the following formula is created on a website whose culture setting is fr-fr (France): =IF(Number1>Number2;5;10). If the website's culture is then changed to en-us (United States), the formula changes automatically to: =IF(Number1>Number2,5,10).

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#conditional-formulas)Conditional formulas

You can use the following formulas to test the condition of a statement and return a Yes or No value, to test an alternate value such as OK or Not OK, or to return a blank or dash to represent a null value.

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#determine-whether-a-number-is-greater-than-or-less-than-another-number)Determine whether a number is greater than or less than another number

Use the IF function to perform this comparison.

|     |     |     |     |
| --- | --- | --- | --- |Determine whether a number is greater than or less than another number 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 15000 | 9000 | =\[Column1\]>\[Column2\] | Is Column1 greater than Column2? (Yes) |
| 15000 | 9000 | =IF(\[Column1\]<=\[Column2\], "OK", "Not OK") | Is Column1 less than or equal to Column2? (Not OK) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#return-a-logical-value-after-comparing-column-contents)Return a logical value after comparing column contents

For a result that is a logical value (Yes or No), use the AND, OR, and NOT functions.

|     |     |     |     |     |
| --- | --- | --- | --- | --- |Return a logical value after comparing column contents 
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 15  | 9   | 8   | =AND(\[Column1\]>\[Column2\], \[Column1\]<\[Column3\]) | Is 15 greater than 9 and less than 8? (No) |
| 15  | 9   | 8   | =OR(\[Column1\]>\[Column2\], \[Column1\]<\[Column3\]) | Is 15 greater than 9 or less than 8? (Yes) |
| 15  | 9   | 8   | =NOT(\[Column1\]+\[Column2\]=24) | Is 15 plus 9 not equal to 24? (No) |

For a result that is another calculation, or any other value other than Yes or No, use the IF, AND, and OR functions.

|     |     |     |     |     |
| --- | --- | --- | --- | --- |Return a logical value after comparing column contents 
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 15  | 9   | 8   | =IF(\[Column1\]=15, "OK", "Not OK") | If the value in Column1 equals 15, return "OK". (OK) |
| 15  | 9   | 8   | =IF(AND(\[Column1\]>\[Column2\], \[Column1\]<\[Column3\]), "OK", "Not OK") | If 15 is greater than 9 and less than 8, return "OK". (Not OK) |
| 15  | 9   | 8   | =IF(OR(\[Column1\]>\[Column2\], \[Column1\]<\[Column3\]), "OK", "Not OK") | If 15 is greater than 9 or less than 8, return "OK". (OK) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#display-zeroes-as-blanks-or-dashes)Display zeroes as blanks or dashes

To display a zero, perform a simple calculation. To display a blank or a dash, use the IF function.

|     |     |     |     |
| --- | --- | --- | --- |Display zeroes as blanks or dashes 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 10  | 10  | =\[Column1\]-\[Column2\] | Second number subtracted from the first. (0) |
| 15  | 9   | =IF(\[Column1\]-\[Column2\],\[Column1\]-\[Column2\],"-") | Returns a dash when the value is zero. (-) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#hide-error-values-in-columns)Hide error values in columns

To display a dash, #N/A, or NA in place of an error value, use the ISERROR function.

|     |     |     |     |
| --- | --- | --- | --- |Hide error values in columns 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 10  | 0   | =\[Column1\]/\[Column2\] | Results in an error (#DIV/0) |
| 10  | 0   | =IF(ISERROR(\[Column1\]/\[Column2\]),"NA",\[Column1\]/\[Column2\]) | Returns NA when the value is an error |
| 10  | 0   | =IF(ISERROR(\[Column1\]/\[Column2\]),"-",\[Column1\]/\[Column2\]) | Returns a dash when the value is an error |

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#date-and-time-formulas)Date and time formulas

You can use the following formulas to perform calculations that are based on dates and times, such as adding a number of days, months, or years to a date, calculating the difference between two dates, and converting time to a decimal value.

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#add-dates)Add dates

To add a number of days to a date, use the addition (+) operator.

Note

When you manipulate dates, the return type of the calculated column must be set to Date and Time.

|     |     |     |     |
| --- | --- | --- | --- |Add dates 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 6/9/2007 | 3   | =\[Column1\]+\[Column2\] | Adds 3 days to 6/9/2007 (6/12/2007) |
| 12/10/2008 | 54  | =\[Column1\]+\[Column2\] | Adds 54 days to 12/10/2008 (2/2/2009) |

To add a number of months to a date, use the DATE, YEAR, MONTH, and DAY functions.

|     |     |     |     |
| --- | --- | --- | --- |Add dates 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 6/9/2007 | 3   | =DATE(YEAR(\[Column1\]),MONTH(\[Column1\])+\[Column2\],DAY(\[Column1\])) | Adds 3 months to 6/9/2007 (9/9/2007) |
| 12/10/2008 | 25  | =DATE(YEAR(\[Column1\]),MONTH(\[Column1\])+\[Column2\],DAY(\[Column1\])) | Adds 25 months to 12/10/2008 (1/10/2011) |

To add a number of years to a date, use the DATE, YEAR, MONTH, and DAY functions.

|     |     |     |     |
| --- | --- | --- | --- |Table 8 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 6/9/2007 | 3   | =DATE(YEAR(\[Column1\])+\[Column2\],MONTH(\[Column1\]),DAY(\[Column1\])) | Adds 3 years to 6/9/2007 (6/9/2010) |
| 12/10/2008 | 25  | =DATE(YEAR(\[Column1\])+\[Column2\],MONTH(\[Column1\]),DAY(\[Column1\])) | Adds 25 years to 12/10/2008 (12/10/2033) |

To add a combination of days, months, and years to a date, use the DATE, YEAR, MONTH, and DAY functions.

|     |     |     |
| --- | --- | --- |Table 9 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 6/9/2007 | =DATE(YEAR(\[Column1\])+3,MONTH(\[Column1\])+1,DAY(\[Column1\])+5) | Adds 3 years, 1 month, and 5 days to 6/9/2007 (7/14/2010) |
| 12/10/2008 | =DATE(YEAR(\[Column1\])+1,MONTH(\[Column1\])+7,DAY(\[Column1\])+5) | Adds 1 year, 7 months, and 5 days to 12/10/2008 (7/15/2010) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-difference-between-two-dates)Calculate the difference between two dates

Use the DATEDIF function to perform this calculation.

|     |     |     |     |
| --- | --- | --- | --- |Calculate the difference between two dates 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 01-Jan-1995 | 15-Jun-1999 | =DATEDIF(\[Column1\], \[Column2\],"d") | Returns the number of days between the two dates (1626) |
| 01-Jan-1995 | 15-Jun-1999 | =DATEDIF(\[Column1\], \[Column2\],"ym") | Returns the number of months between the dates, ignoring the year part (5) |
| 01-Jan-1995 | 15-Jun-1999 | =DATEDIF(\[Column1\], \[Column2\],"yd") | Returns the number of days between the dates, ignoring the year part (165) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-difference-between-two-times)Calculate the difference between two times

To present the result in the standard time format (hours:minutes:seconds), use the subtraction operator (-) and the TEXT function. For this method to work, hours must not exceed 24, and minutes and seconds must not exceed 60.

|     |     |     |     |
| --- | --- | --- | --- |Calculate the difference between two times 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 06/09/2007 10:35 AM | 06/09/2007 3:30 PM | =TEXT(\[Column2\]-\[Column1\],"h") | Hours between two times (4) |
| 06/09/2007 10:35 AM | 06/09/2007 3:30 PM | =TEXT(\[Column2\]-\[Column1\],"h:mm") | Hours and minutes between two times (4:55) |
| 06/09/2007 10:35 AM | 06/09/2007 3:30 PM | =TEXT(\[Column2\]-\[Column1\],"h:mm:ss") | Hours, minutes, and seconds between two times (4:55:00) |

To present the result in a total that is based on one time unit, use the INT function, or HOUR, MINUTE, or SECOND function.

|     |     |     |     |
| --- | --- | --- | --- |Calculate the difference between two times 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =INT((\[Column2\]-\[Column1\])*24) | Total hours between two times (28) |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =INT((\[Column2\]-\[Column1\])*1440) | Total minutes between two times (1735) |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =INT((\[Column2\]-\[Column1\])*86400) | Total seconds between two times (104100) |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =HOUR(\[Column2\]-\[Column1\]) | Hours between two times, when the difference does not exceed 24 (4) |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =MINUTE(\[Column2\]-\[Column1\]) | Minutes between two times, when the difference does not exceed 60 (55) |
| 06/09/2007 10:35 AM | 06/10/2007 3:30 PM | =SECOND(\[Column2\]-\[Column1\]) | Seconds between two times, when the difference does not exceed 60 (0) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#convert-times)Convert times

To convert hours from the standard time format to a decimal number, use the INT function.

|     |     |     |
| --- | --- | --- |Convert times 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 10:35 AM | =(\[Column1\]-INT(\[Column1\]))*24 | Number of hours since 12:00 AM (10.583333) |
| 12:15 PM | =(\[Column1\]-INT(\[Column1\]))*24 | Number of hours since 12:00 AM (12.25) |

To convert hours from a decimal number to the standard time format (hours:minutes:seconds), use the division operator and the TEXT function.

|     |     |     |
| --- | --- | --- |Convert times 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 23:58 | =TEXT(Column1/24, "hh:mm:ss") | Hours, minutes, and seconds since 12:00 AM (00:59:55) |
| 2:06 | =TEXT(Column1/24, "h:mm") | Hours and minutes since 12:00 AM (0:05) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#insert-julian-dates)Insert Julian dates

A Julian date refers to a date format that is a combination of the current year and the number of days since the beginning of the year. For example, January 1, 2007, is represented as 2007001 and December 31, 2007, is represented as 2007365. This format is not based on the Julian calendar.

To convert a date to a Julian date, use the TEXT and DATEVALUE functions.

|     |     |     |
| --- | --- | --- |Insert Julian dates 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 6/23/2007 | =TEXT(\[Column1\],"yy")&TEXT((\[Column1\]-DATEVALUE("1/1/"& TEXT(\[Column1\],"yy"))+1),"000") | Date in Julian format, with a two-digit year (07174) |
| 6/23/2007 | =TEXT(\[Column1\],"yyyy")&TEXT((\[Column1\]-DATEVALUE("1/1/"&TEXT(\[Column1\],"yy"))+1),"000") | Date in Julian format, with a four-digit year (2007174) |

To convert a date to a Julian date that is used in astronomy, use the constant 2415018.50. This formula works only for dates after 3/1/1901, and if you are using the 1900 date system.

|     |     |     |
| --- | --- | --- |Insert Julian dates 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 6/23/2007 | =\[Column1\]+2415018.50 | Date in Julian format, used in astronomy (2454274.50) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#show-dates-as-the-day-of-the-week)Show dates as the day of the week

To convert dates to the text for the day of the week, use the TEXT and WEEKDAY functions.

|     |     |     |
| --- | --- | --- |Show dates as the day of the week 
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 19-Feb-2007 | =TEXT(WEEKDAY(\[Column1\]), "dddd") | Calculates the day of the week for the date and returns the full name of the day (Monday) |
| 3-Jan-2008 | =TEXT(WEEKDAY(\[Column1\]), "ddd") | Calculates the day of the week for the date and returns the abbreviated name of the day (Thu) |

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#mathematical-formulas)Mathematical formulas

You can use the following formulas to perform a variety of mathematical calculations, such as adding, subtracting, multiplying, and dividing numbers; calculating the average or median of numbers; rounding a number; and counting values.

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#add-numbers)Add numbers

To add numbers in two or more columns in a row, use the addition operator (+) or the SUM function.

|     |     |     |     |     |
| --- | --- | --- | --- | --- |Add numbers 
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 6   | 5   | 4   | =\[Column1\]+\[Column2\]+\[Column3\] | Adds the values in the first three columns (15) |
| 6   | 5   | 4   | =SUM(\[Column1\],\[Column2\],\[Column3\]) | Adds the values in the first three columns (15) |
| 6   | 5   | 4   | =SUM(IF(\[Column1\]>\[Column2\], \[Column1\]-\[Column2\], 10), \[Column3\]) | If Column1 is greater than Column2, adds the difference and Column3. Else add 10 and Column3 (5) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#subtract-numbers)Subtract numbers

To subtract numbers in two or more columns in a row, use the subtraction operator (-) or the SUM function with negative numbers.

|     |     |     |     |     |
| --- | --- | --- | --- | --- |Subtract numbers 
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 15000 | 9000 | -8000 | =\[Column1\]-\[Column2\] | Subtracts 9000 from 15000 (6000) |
| 15000 | 9000 | -8000 | =SUM(\[Column1\], \[Column2\], \[Column3\]) | Adds numbers in the first three columns, including negative values (16000) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-difference-between-two-numbers-as-a-percentage)Calculate the difference between two numbers as a percentage

Use the subtraction (-) and division (/) operators and the ABS function.

|     |     |     |     |
| --- | --- | --- | --- |Calculate the difference between two numbers as a percentage 
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 2342 | 2500 | =(\[Column2\]-\[Column1\])/ABS(\[Column1\]) | Percentage change (6.75% or 0.06746) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#multiply-numbers)Multiply numbers

To multiply numbers in two or more columns in a row, use the multiplication operator (*) or the PRODUCT function.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 5   | 2   | =\[Column1\]*\[Column2\] | Multiplies the numbers in the first two columns (10) |
| 5   | 2   | =PRODUCT(\[Column1\], \[Column2\]) | Multiplies the numbers in the first two columns (10) |
| 5   | 2   | =PRODUCT(\[Column1\],\[Column2\],2) | Multiplies the numbers in the first two columns and the number 2 (20) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#divide-numbers)Divide numbers

To divide numbers in two or more columns in a row, use the division operator (/).

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 15000 | 12  | =\[Column1\]/\[Column2\] | Divides 15000 by 12 (1250) |
| 15000 | 12  | =(\[Column1\]+10000)/\[Column2\] | Adds 15000 and 10000, and then divides the total by 12 (2083) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-average-of-numbers)Calculate the average of numbers

The average is also called the mean. To calculate the average of numbers in two or more columns in a row, use the AVERAGE function.

  
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 6   | 5   | 4   | =AVERAGE(\[Column1\], \[Column2\],\[Column3\]) | Average of the numbers in the first three columns (5) |
| 6   | 5   | 4   | =AVERAGE(IF(\[Column1\]>\[Column2\], \[Column1\]-\[Column2\], 10), \[Column3\]) | If Column1 is greater than Column2, calculate the average of the difference and Column3. Else calculate the average of the value 10 and Column3 (2.5) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-median-of-numbers)Calculate the median of numbers

The median is the value at the center of an ordered range of numbers. Use the MEDIAN function to calculate the median of a group of numbers.

  
| A   | B   | C   | D   | E   | F   | Formula | Description (result) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 10  | 7   | 9   | 27  | 0   | 4   | =MEDIAN(A, B, C, D, E, F) | Median of numbers in the first 6 columns (8) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#calculate-the-smallest-or-largest-number-in-a-range)Calculate the smallest or largest number in a range

To calculate the smallest or largest number in two or more columns in a row, use the MIN and MAX functions.

  
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| 10  | 7   | 9   | =MIN(\[Column1\], \[Column2\], \[Column3\]) | Smallest number (7) |
| 10  | 7   | 9   | =MAX(\[Column1\], \[Column2\], \[Column3\]) | Largest number (10) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#count-values)Count values

To count numeric values, use the COUNT function.

  
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| Apple |     | 12/12/2007 | =COUNT(\[Column1\], \[Column2\], \[Column3\]) | Counts the number of columns that contain numeric values. Excludes date and time, text, and null values (0) |
| $12 | #DIV/0! | 1.01 | =COUNT(\[Column1\], \[Column2\], \[Column3\]) | Counts the number of columns that contain numeric values, but excludes error and logical values (2) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#increase-or-decrease-a-number-by-a-percentage)Increase or decrease a number by a percentage

Use the percent (%) operator to perform this calculation.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 23  | 3%  | =\[Column1\]*(1+5%) | Increases number in Column1 by 5% (24.15) |
| 23  | 3%  | =\[Column1\]*(1+\[Column2\]) | Increases number in Column1 by the percent value in Column2: 3% (23.69) |
| 23  | 3%  | =\[Column1\]*(1-\[Column2\]) | Decreases number in Column1 by the percent value in Column2: 3% (22.31) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#raise-a-number-to-a-power)Raise a number to a power

Use the exponentiation operator (^) or the POWER function to perform this calculation.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| 5   | 2   | =\[Column1\]^\[Column2\] | Calculates five squared (25) |
| 5   | 3   | =POWER(\[Column1\], \[Column2\]) | Calculates five cubed (125) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#round-a-number)Round a number

To round up a number, use the ROUNDUP, ODD, or EVEN function.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 20.3 | =ROUNDUP(\[Column1\],0) | Rounds 20.3 up to the nearest whole number (21) |
| -5.9 | =ROUNDUP(\[Column1\],0) | Rounds -5.9 up to the nearest whole number (-5) |
| 12.5493 | =ROUNDUP(\[Column1\],2) | Rounds 12.5493 up to the nearest hundredth, two decimal places (12.55) |
| 20.3 | =EVEN(\[Column1\]) | Rounds 20.3 up to the nearest even number (22) |
| 20.3 | =ODD(\[Column1\]) | Rounds 20.3 up to the nearest odd number (21) |

To round down a number, use the ROUNDDOWN function.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 20.3 | =ROUNDDOWN(\[Column1\],0) | Rounds 20.3 down to the nearest whole number (20) |
| -5.9 | =ROUNDDOWN(\[Column1\],0) | Rounds -5.9 down to the nearest whole number (-6) |
| 12.5493 | =ROUNDDOWN(\[Column1\],2) | Rounds 12.5493 down to the nearest hundredth, two decimal places (12.54) |

To round a number to the nearest number or fraction, use the ROUND function.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 20.3 | =ROUND(\[Column1\],0) | Rounds 20.3 down, because the fractional part is less than .5 (20) |
| 5.9 | =ROUND(\[Column1\],0) | Rounds 5.9 up, because the fractional part is greater than .5 (6) |
| -5.9 | =ROUND(\[Column1\],0) | Rounds -5.9 down, because the fractional part is less than -.5 (-6) |
| 1.25 | =ROUND(\[Column1\], 1) | Rounds the number to the nearest tenth (one decimal place). Because the portion to be rounded is 0.05 or greater, the number is rounded up (result: 1.3) |
| 30.452 | =ROUND(\[Column1\], 2) | Rounds the number to the nearest hundredth (two decimal places). Because the portion to be rounded, 0.002, is less than 0.005, the number is rounded down (result: 30.45) |

To round a number to the significant digit above 0, use the ROUND, ROUNDUP, ROUNDDOWN, INT, and LEN functions.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| 5492820 | =ROUND(\[Column1\],3-LEN(INT(\[Column1\]))) | Rounds the number to 3 significant digits (5490000) |
| 22230 | =ROUNDDOWN(\[Column1\],3-LEN(INT(\[Column1\]))) | Rounds the bottom number down to 3 significant digits (22200) |
| 5492820 | =ROUNDUP(\[Column1\], 5-LEN(INT(\[Column1\]))) | Rounds the top number up to 5 significant digits (5492900) |

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#text-formulas)Text formulas

You can use the following formulas to manipulate text, such as combining or concatenating the values from multiple columns, comparing the contents of columns, removing characters or spaces, and repeating characters.

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#change-the-case-of-text)Change the case of text

To change the case of text, use the UPPER, LOWER, or PROPER function.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| nina Vietzen | =UPPER(\[Column1\]) | Changes text to uppercase (NINA VIETZEN) |
| nina Vietzen | =LOWER(\[Column1\]) | Changes text to lowercase (nina vietzen) |
| nina Vietzen | =PROPER(\[Column1\]) | Changes text to title case (Nina Vietzen) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#combine-first-and-last-names)Combine first and last names

To combine first and last names, use the ampersand operator (&) or the CONCATENATE function.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| Carlos | Carvallo | =\[Column1\]&\[Column2\] | Combines the two strings (CarlosCarvallo) |
| Carlos | Carvallo | =\[Column1\]&" "&\[Column2\] | Combines the two strings, separated by a space (Carlos Carvallo) |
| Carlos | Carvallo | =\[Column2\]&", "&\[Column1\] | Combines the two strings, separated by a comma and a space (Carvallo, Carlos) |
| Carlos | Carvallo | =CONCATENATE(\[Column2\], ",", \[Column1\]) | Combines the two strings, separated by a comma (Carvallo,Carlos) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#combine-text-and-numbers-from-different-columns)Combine text and numbers from different columns

To combine text and numbers, use the CONCATENATE function, the ampersand operator (&), or the TEXT function and the ampersand operator.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| Yang | 28  | =\[Column1\]&" sold "&\[Column2\]&" units." | Combines contents above into a phrase (Yang sold 28 units.) |
| Dubois | 40% | =\[Column1\]&" sold "&TEXT(\[Column2\],"0%")&" of the total sales." | Combines contents above into a phrase (Dubois sold 40% of the total sales.)<br><br>**Note**   The TEXT function appends the formatted value of Column2 instead of the underlying value, which is 0.4. |
| Yang | 28  | =CONCATENATE(\[Column1\]," sold ",\[Column2\]," units.") | Combines contents above into a phrase (Yang sold 28 units.) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#combine-text-with-a-date-or-time)Combine text with a date or time

To combine text with a date or time, use the TEXT function and the ampersand operator (&).

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| Billing Date | 5-Jun-2007 | ="Statement date: "&TEXT(\[Column2\], "d-mmm-yyyy") | Combines text with a date (Statement date: 5-Jun-2007) |
| Billing Date | 5-Jun-2007 | =\[Column1\]&" "&TEXT(\[Column2\], "mmm-dd-yyyy") | Combines text and date from different columns into one column (Billing Date Jun-05-2007) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#compare-column-contents)Compare column contents

To compare one column to another column or a list of values, use the EXACT and OR functions.

  
| Column1 | Column2 | Formula | Description (possible result) |
| --- | --- | --- | --- |
| BD122 | BD123 | =EXACT(\[Column1\],\[Column2\]) | Compares contents of first two columns (No) |
| BD122 | BD123 | =EXACT(\[Column1\], "BD122") | Compares contents of Column1 and the string "BD122" (Yes) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#determine-whether-a-column-value-or-a-part-of-it-matches-specific-text)Determine whether a column value or a part of it matches specific text

To determine whether a column value or a part of it matches specific text, use the IF, FIND, SEARCH, and ISNUMBER functions.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| Vietzen | =IF(\[Column1\]="Vietzen", "OK", "Not OK") | Determines whether Column1 is Vietzen (OK) |
| Vietzen | =IF(ISNUMBER(FIND("v",\[Column1\])), "OK", "Not OK") | Determines whether Column1 contains the letter v (OK) |
| BD123 | =ISNUMBER(FIND("BD",\[Column1\])) | Determines whether Column1 contains BD (Yes) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#count-nonblank-columns)Count nonblank columns

To count nonblank columns, use the COUNTA function.

  
| Column1 | Column2 | Column3 | Formula | Description (possible result) |
| --- | --- | --- | --- | --- |
| Sales | 19  |     | =COUNTA(\[Column1\], \[Column2\]) | Counts the number of nonblank columns (2) |
| Sales | 19  |     | =COUNTA(\[Column1\], \[Column2\], \[Column3\]) | Counts the number of nonblank columns (2) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#remove-characters-from-text)Remove characters from text

To remove characters from text, use the LEN, LEFT, and RIGHT functions.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| Vitamin A | =LEFT(\[Column1\],LEN(\[Column1\])-2) | Returns 7 (9-2) characters, starting from left (Vitamin) |
| Vitamin B1 | =RIGHT(\[Column1\], LEN(\[Column1\])-8) | Returns 2 (10-8) characters, starting from right (B1) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#remove-spaces-from-the-beginning-and-end-of-a-column)Remove spaces from the beginning and end of a column

To remove spaces from a column, use the TRIM function.

  
| Column1 | Formula | Description (possible result) |
| --- | --- | --- |
| Hello there! | =TRIM(\[Column1\]) | Removes the spaces from the beginning and end (Hello there!) |

### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#repeat-a-character-in-a-column)Repeat a character in a column

To repeat a character in a column, use the REPT function.

  
| Formula | Description (possible result) |
| --- | --- |
| =REPT(".",3) | Repeats a period 3 times (...) |
| =REPT("-",10) | Repeats a dash 10 times (----------) |

## [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#see-also)See Also

#### [](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/bb862071(v=office.14)?redirectedfrom=MSDN#reference)Reference

[SPFieldCalculated](https://docs.microsoft.com/en-us/previous-versions/office/developer/sharepoint-2010/ms415687(v=office.14))