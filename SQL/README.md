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

## System, connection and users

#### Find and kill active connections
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
WHERE  sysd.NAME LIKE '%miroglio%' 

-- Killing a process by SPID
-- KILL spid
```

#### Find tables that have at least 1 row
```sql
SELECT NAME AS table_name, Sum(row_count) AS row_count
FROM   sys.dm_db_partition_stats p JOIN sys.objects o
       ON o.object_id = p.object_id
WHERE  o.type NOT IN ( 'S', 'IT' )
GROUP  BY NAME,row_count
HAVING Sum(row_count) > 0
```
