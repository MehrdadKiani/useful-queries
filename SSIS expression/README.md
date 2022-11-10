# SSIS expression collection

## Date and Time

#### Get the current day full name. e.g. Monday or Tuesday:
```sql
(
DATEPART("dw", GETDATE()) == 1 ? "Sunday"     : 
DATEPART("dw", GETDATE()) == 2 ? "Monday"     :
DATEPART("dw", GETDATE()) == 3 ? "Tuesday"    : 
DATEPART("dw", GETDATE()) == 4 ? "Wednesday"  :
DATEPART("dw", GETDATE()) == 5 ? "Thursday"   : 
DATEPART("dw", GETDATE()) == 6 ? "Friday"     :
DATEPART("dw", GETDATE()) == 7 ? "Saturday" : "InvalidDay"
)
```
