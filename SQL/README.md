# SQL collection

## Date and Time

#### Find the last week's day as Date
```sql
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+0)%7, GETDATE()) -- Last Saturday
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+1)%7, GETDATE()) -- Last Fridays
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+2)%7, GETDATE()) -- Last Thursdays
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+3)%7, GETDATE()) -- Last Wednesday
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+4)%7, GETDATE()) -- Last Tuesday
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+5)%7, GETDATE()) -- Last Monday
SELECT DATEADD(DD,-(DATEPART(WEEKDAY, GETDATE())+6)%7, GETDATE()) -- Last Sunday
```

## Others

#### Find active connections
```sql
SELECT sysp.spid,
       sysd.NAME,
       sysd.database_id,
       sysp.cpu,
       sysp.physical_io,
       sysp.memusage,
       sysp.login_time,
       sysp.last_batch,
       sysp.hostname,
       sysp.program_name,
       sysp.hostprocess,
       sysp.loginame,
       syss.original_login_name
FROM   sys.databases sysd
       JOIN sys.sysprocesses sysp
         ON sysd.database_id = sysp.dbid
       JOIN sys.dm_exec_sessions syss
         ON sysp.dbid = syss.session_id
WHERE  sysd.NAME LIKE '%DBNAME%' 
```
