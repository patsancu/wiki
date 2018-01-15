### Character set mismatch in a case expression
[Source](https://stackoverflow.com/a/10521505)
Maybe it's a mismatch between an NVARCHAR and a regular VARCHAR, like in the following example, where t.First_Col is a NVARCHAR and the string it's being compared to is a regular string (Varchar).
```sql
CASE WHEN t.First_Col = 'ItemOne'
       THEN 'anItemOne'
       WHEN t.First_Col = 'ItemTwo'
       THEN CASE WHEN t.Second_Col = 'ItemTwo_A'
                 THEN 'aSecondItem_A'
                 ELSE 'aSecondItem'
                 END
ELSE 'NoItem'
END
```
Add a n prefix, like this:
```sql
CASE WHEN t.First_Col = N'ItemOne'
   THEN N'anItemOne'
   WHEN t.First_Col = N'ItemTwo'
   THEN (CASE WHEN t.Second_Col = N'ItemTwo_A'
              THEN N'aSecondItem_A'
              ELSE N'aSecondItem'
         END)
   ELSE N'NoItem'
END
```
