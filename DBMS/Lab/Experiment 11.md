# DBMS Lab Experiment 11
## To understand the concepts of index
---
- **Course:** [[DBMS]]
- **Name:** Devesh Chandra Srivastava
- **SapID:** 590017127
- **Batch:** 66
- **Semester:** 3
- **Date:** 2025-09-08

---

1) Create an index of name `employee_idx` on `EMPLOYEES` with column
`Last_Name`, `Department_id`

```sql
CREATE INDEX employee_idx ON EMPLOYEES (Last_Name, Department_id);
```

2) Find the `ROWID` for the above table and create a unique index on `employee_id`
Column of the `EMPLOYE0ES`.

```sql
SELECT ctid, Employee_id FROM EMPLOYEES;

CREATE UNIQUE INDEX emp_unique_idx ON EMPLOYEES (Employee_id);

```

#### Result
![[Pasted image 20251110143513.png]]

3) Create a reverse index on `employee_id` column of the `EMPLOYEES`.

```
CREATE INDEX emp_reverse_idx ON EMPLOYEES (REVERSE(Employee_id));
```

4) Create a unique and composite index on `employee_id` and check whether there
Is duplicity of tuples or not.

```sql
CREATE UNIQUE INDEX emp_composite_idx ON EMPLOYEES (Employee_id, Department_id);

SELECT Employee_id, Department_id, COUNT(*) 
FROM EMPLOYEES 
GROUP BY Employee_id, Department_id 
HAVING COUNT(*) > 1;
```

5) Create Function-based indexes defined on the SQL functions
UPPER (`column_name`) or LOWER (`column_name`) to facilitate case-insensitive
Searches (on column `Last_Name`).

```sql
CREATE INDEX emp_lastname_upper_idx ON EMPLOYEES (UPPER(Last_Name));
```

6) Drop the function based index on column `Last_Name`.

```sql
DROP INDEX emp_lastname_upper_idx;
```


### Comparison between indexing and non indexing

1) Query to insert 10,000 values  

```sql 
CREATE TABLE employees (
    employee_id   SERIAL PRIMARY KEY,
    first_name    VARCHAR(30) NOT NULL,
    last_name     VARCHAR(30) NOT NULL,
    dob           DATE,
    salary        NUMERIC(10, 2),
    department_id INT
);
```

```sql
INSERT INTO employees (first_name, last_name, dob, salary, department_id)
SELECT
    'First_' || g,
    'Last_' || (g % 500),
    DATE '1980-01-01' + (g % 1000),
    (30000 + (random() * 50000))::NUMERIC(10,2),
    (1 + (g % 10))
FROM generate_series(1, 10000) AS g;

```


2) Analysing without indexing
```sql
EXPLAIN ANALYZE SELECT * FROM employees WHERE last_name = 'Last_250';
```
#### Result

![[Pasted image 20251110151915.png]]

3) Create Index
```sql 
CREATE INDEX emp_lastname_idx ON employees (last_name);
EXPLAIN ANALYZE SELECT * FROM employees WHERE last_name = 'Last_250';
```

#### Results

![[Pasted image 20251110152300.png]]

### Comparison

| Test Case         | Planning Time | Execution Time |
| ----------------- | ------------- | -------------- |
| **Without Index** | 0.200 ms      | **2.000 ms**   |
| **With Index**    | 0.400 ms      | **0.100 ms**   |
