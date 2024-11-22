# [MySQL Manual](https://dev.mysql.com/doc/refman/8.4/en/)

## 1. Database Operations

### Create a Database:
```sql
CREATE DATABASE database_name;
```

### Show Databases:
```sql
SHOW DATABASES;
```

### Use a Database:
```sql
USE database_name;
```

### Drop a Database:
```sql
DROP DATABASE database_name;
```

## 2. Table Operations

### Create a Table:
```sql
CREATE TABLE table_name (
    column1 datatype PRIMARY KEY,
    column2 datatype,
    column3 datatype
);
```

### Show Tables:
```sql
SHOW TABLES;
```

### Describe Table Structure:
```sql
DESCRIBE table_name;
```

### Drop a Table:
```sql
DROP TABLE table_name;
```

## 3. Inserting Data

### Insert Data into Table:
```sql
INSERT INTO table_name (column1, column2, column3)
VALUES (value1, value2, value3);
```

## 4. Selecting Data

### Select All Data:
```sql
SELECT * FROM table_name;
```

### Select Specific Columns:
```sql
SELECT column1, column2 FROM table_name;
```

### Where Clause (Filtering):
```sql
SELECT * FROM table_name WHERE column1 = 'value';
```

### Order Data (Ascending/Descending):
```sql
SELECT * FROM table_name ORDER BY column1 ASC;
SELECT * FROM table_name ORDER BY column1 DESC;
```

### Limit Results:
```sql
SELECT * FROM table_name LIMIT 5;
```

## 5. Updating Data

### Update a Record:
```sql
UPDATE table_name SET column1 = 'new_value' WHERE column2 = 'some_value';
```

## 6. Deleting Data

### Delete Data:
```sql
DELETE FROM table_name WHERE column = 'value';
```

## 7. Joining Tables

### Inner Join (Returns matching records from both tables):
```sql
SELECT * FROM table1
INNER JOIN table2 ON table1.id = table2.id;
```

### Left Join (Returns all records from the left table, and matched records from the right table):
```sql
SELECT * FROM table1
LEFT JOIN table2 ON table1.id = table2.id;
```

## 8. Aggregating Data

### Count Rows:
```sql
SELECT COUNT(*) FROM table_name;
```

### Sum Values:
```sql
SELECT SUM(column_name) FROM table_name;
```

### Average Values:
```sql
SELECT AVG(column_name) FROM table_name;
```

## 9. Group By and Having

### Group By (Group rows sharing a property):
```sql
SELECT column1, COUNT(*) FROM table_name GROUP BY column1;
```

### Having (Filter groups based on an aggregate):
```sql
SELECT column1, COUNT(*) FROM table_name GROUP BY column1 HAVING COUNT(*) > 10;
```

## 10. Indexes

### Create an Index:
```sql
CREATE INDEX index_name ON table_name (column_name);
```

### Show Indexes:
```sql
SHOW INDEXES FROM table_name;
```

## 11. Constraints

### Primary Key (Uniquely identifies a record):
```sql
CREATE TABLE table_name (
    id INT AUTO_INCREMENT,
    column1 VARCHAR(100),
    PRIMARY KEY(id)
);
```

### Foreign Key (Links two tables):
```sql
CREATE TABLE table_name (
    id INT,
    other_table_id INT,
    FOREIGN KEY (other_table_id) REFERENCES other_table(id)
);
```

## 12. Backup and Restore

### Backup a Database (via command line):
```bash
mysqldump -u username -p database_name > backup.sql
```

### Restore a Database:
```bash
mysql -u username -p database_name < backup.sql
```

## 13. User and Permissions

### Create a New User:
```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

### Grant Permissions:
```sql
GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
```

### Show Current Users:
```sql
SELECT User, Host FROM mysql.user;
```

### Revoke Permissions:
```sql
REVOKE ALL PRIVILEGES ON database_name.* FROM 'username'@'localhost';
```

## 14. Backup Management

### Show Databases:
```sql
SHOW DATABASES;
```

### Show Tables in a Database:
```sql
SHOW TABLES;
```
