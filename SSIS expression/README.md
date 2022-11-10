# SSIS expression collection

## Date and Time

- **Current Day Short Name (ddd)**: Get the current day full name. e.g. Monday or Tuesday:
```sql
(
DATEPART("dw", GETDATE()) == 1 ? "Sunday" : 
DATEPART("dw", GETDATE()) == 2 ? "Monday" :
DATEPART("dw", GETDATE()) == 3 ? "Tuesday" : 
DATEPART("dw", GETDATE()) == 4 ? "Wednesday" :
DATEPART("dw", GETDATE()) == 5 ? "Thursday" : 
DATEPART("dw", GETDATE()) == 6 ? "Friday" :
DATEPART("dw", GETDATE()) == 7 ? "Saturday" : "InvalidDay"
)
```

- **Current Day Full Name (dddd)**: Get the current day short name. e.g. Mon, Tue
```sql
(
DATEPART("dw", GETDATE()) == 1 ? "Sun" : 
DATEPART("dw", GETDATE()) == 2 ? "Mon" :
DATEPART("dw", GETDATE()) == 3 ? "Tue" : 
DATEPART("dw", GETDATE()) == 4 ? "Wed" :
DATEPART("dw", GETDATE()) == 5 ? "Thu" : 
DATEPART("dw", GETDATE()) == 6 ? "Fri" :
DATEPART("dw", GETDATE()) == 7 ? "Sat" : "InvalidDay"
)
```

- **Current Month Full Name (mmmm)**: Get the current month full name. On the 1st January, the expression will return 'January'.
```sql
(
MONTH(GETDATE()) == 1 ? "January" : 
MONTH(GETDATE()) == 2 ? "February" : 
MONTH(GETDATE()) == 3 ? "March" :
MONTH(GETDATE()) == 4 ? "April" : 
MONTH(GETDATE()) == 5 ? "May" : 
MONTH(GETDATE()) == 6 ? "June" :
MONTH(GETDATE()) == 7 ? "July" : 
MONTH(GETDATE()) == 8 ? "August" : 
MONTH(GETDATE()) == 9 ? "September" :
MONTH(GETDATE()) == 10 ? "October" : 
MONTH(GETDATE()) == 11 ? "November" :
MONTH(GETDATE()) == 12 ? "December" : "InvalidMonth"
)
```

- **Current Month Short Name (mmm)**: Get the current month short name. On the 1st January, the expression will return 'Jan'.
```sql
(
MONTH(GETDATE()) == 1 ? "Jan" : 
MONTH(GETDATE()) == 2 ? "Feb" : 
MONTH(GETDATE()) == 3 ? "Mar" :
MONTH(GETDATE()) == 4 ? "Apr" : 
MONTH(GETDATE()) == 5 ? "May" : 
MONTH(GETDATE()) == 6 ? "Jun" :
MONTH(GETDATE()) == 7 ? "Jul" : 
MONTH(GETDATE()) == 8 ? "Aug" : 
MONTH(GETDATE()) == 9 ? "Sep" :
MONTH(GETDATE()) == 10 ? "Oct" : 
MONTH(GETDATE()) == 11 ? "Nov" : 
MONTH(GETDATE()) == 12 ? "Dec" :
"InvalidMonth"
)
```

- **Yesterday Date yyyy-mm-dd**:Yesterday's date in yyyy-mm-dd format.
```sql
(DT_WSTR,4)YEAR(DATEADD("dd", -1, GETDATE())) 
+ "-"
+ RIGHT("0" + (DT_WSTR,2)MONTH(DATEADD("dd", -1, GETDATE())), 2) 
+ "-"
+ RIGHT("0" + (DT_WSTR,2)DAY(DATEADD("dd", -1, GETDATE())), 2)
```

- **Current Date yyyy-mm-dd**:Current date in yyyy-mm-dd format.
```sql
(DT_WSTR,4)YEAR(GETDATE()) 
+ "-"
+ RIGHT("0" + (DT_WSTR,2)MONTH(GETDATE()), 2) 
+ "-"
+ RIGHT("0" + (DT_WSTR,2)DAY( GETDATE()), 2)
```
