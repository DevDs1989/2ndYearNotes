# Lab Experiment 05
# To understand and use SQL Sub-Query
---
- Course: DBMS
- Name: Devesh Chandra Srivastava
- SapID: 590017127
- Batch: 66
- Semester: 3
- Date: 2025-11-11
---

1. Table Creation

Creating SUPPLIER Table
```sql
CREATE TABLE SUPPLIER (
    scode VARCHAR(10) PRIMARY KEY,
    sname VARCHAR(50) NOT NULL,
    scity VARCHAR(30),
    turnover DECIMAL(10,2)
);
```

Creating PART Table
```sql
CREATE TABLE PART (
    pcode VARCHAR(10) PRIMARY KEY,
    weigh DECIMAL(6,2),
    color VARCHAR(20),
    cost DECIMAL(8,2),
    sellingprice DECIMAL(8,2)
);
```

Creating SUPPLIER_PART Table
```sql
CREATE TABLE SUPPLIER_PART (
    scode VARCHAR(10) NOT NULL,
    pcode VARCHAR(10) NOT NULL,
    qty INT,
    PRIMARY KEY (scode, pcode),
    FOREIGN KEY (scode) REFERENCES SUPPLIER(scode),
    FOREIGN KEY (pcode) REFERENCES PART(pcode)
);
```

---

2. Inserting Sample Data

Data for SUPPLIER
```sql
INSERT INTO SUPPLIER (scode, sname, scity, turnover) VALUES
('S001', 'Alpha Suppliers',    'Bombay', 50.00),
('S002', 'Beta Traders',       'Delhi', 75.00),
('S003', 'Gamma Corporation',  'Bombay', NULL),
('S004', 'Delta Supplies',     'Pune', 120.00),
('S005', 'Epsilon Enterprises','Chennai', 40.00),
('S006', 'Zeta Wholesale',     'Mumbai', 200.00);
```

Data for PART
```sql
INSERT INTO PART (pcode, weigh, color, cost, sellingprice) VALUES
('P001', 10.0, 'Red',   15.00, 25.00),
('P002', 30.0, 'Blue',  20.00, 35.00),
('P003', 28.5, 'Green', 30.00, 45.00),
('P004', 40.0, 'Black', 40.00, 60.00),
('P005', 26.0, 'White', 22.50, 34.00),
('P006', 18.0, 'Yellow',18.00, 28.00);
```

Data for SUPPLIER_PART
```sql
INSERT INTO SUPPLIER_PART (scode, pcode, qty) VALUES
('S001', 'P001',  100),
('S001', 'P002',  150),
('S002', 'P002',   50),
('S002', 'P004',   25),
('S003', 'P002',   25),
('S003', 'P003',   40),
('S004', 'P005',   60),
('S005', 'P003',   20),
('S006', 'P004',  200),
('S006', 'P002',  100);
```

---

3. Exercise on Retrieving Records (SQL Sub-Query Examples)

Q 1: Get the supplier number and part number in ascending order of supplier number
```sql
SELECT scode, pcode FROM SUPPLIER_PART
ORDER BY scode ASC, pcode ASC;
```
Result

| scode | pcode |
|-------|-------|
| S 001  | P 001  |
| S 001  | P 002  |
| S 002  | P 002  |
| S 002  | P 004  |
| S 003  | P 002  |
| S 003  | P 003  |
| S 004  | P 005  |
| S 005  | P 003  |
| S 006  | P 002  |
| S 006  | P 004  |

Q 2: Get the details of supplier who operate from Bombay with turnover 50
```sql
SELECT * FROM SUPPLIER
WHERE scity = 'Bombay' AND turnover = 50.00;
```
Result

| scode | sname          | scity  | turnover |
|-------|----------------|--------|----------|
| S 001  | Alpha Suppliers| Bombay | 50.00    |

Q 3: Get the total number of supplier
```sql
SELECT COUNT(*) AS TotalSuppliers FROM SUPPLIER;
```
Result

| TotalSuppliers |
|----------------|
| 6              |

Q 4: Get the part number weighing between 25 and 35
```sql
SELECT pcode FROM PART
WHERE weigh BETWEEN 25 AND 35;
```
Result

| pcode |
|-------|
| P 002  |
| P 003  |
| P 005  |

Q 5: Get the supplier number whose turnover is null
```sql
SELECT scode FROM SUPPLIER
WHERE turnover IS NULL;
```
Result
| scode |
|-------|
| S 003  |

Q 6: Get the part number that cost 20, 30 or 40 rupees
```sql
SELECT pcode FROM PART
WHERE cost IN (20.00, 30.00, 40.00);
```
Result
| pcode |
|-------|
| P 002  |
| P 003  |
| P 004  |

Q 7: Get the total quantity of part 2 that is supplied
(Assuming "part 2" corresponds to pcode = 'P 002')
```sql
SELECT SUM(qty) AS TotalQty_P002 FROM SUPPLIER_PART
WHERE pcode = 'P002';
```
Result

| TotalQty_P 002 |
|---------------|
| 325           |

Q 8: Get the name of supplier who supply part 2
```sql
SELECT DISTINCT S.sname
FROM SUPPLIER S
JOIN SUPPLIER_PART SP ON S.scode = SP.scode
WHERE SP.pcode = 'P002';
```
Result

| sname               |
|---------------------|
| Alpha Suppliers     |
| Beta Traders        |
| Gamma Corporation   |
| Zeta Wholesale      |

Q 9: Get the part number whose cost is greater than the average cost
```sql
SELECT pcode FROM PART
WHERE cost > (SELECT AVG(cost) FROM PART);
```
Result

| pcode |
|-------|
| P 003  |
| P 004  |

Q 10: Get the supplier number and turnover in descending order of turnover
```sql
SELECT scode, turnover FROM SUPPLIER
ORDER BY turnover DESC NULLS LAST;
```
Result

| scode | turnover |
|-------|----------|
| S 006  | 200.00   |
| S 004  | 120.00   |
| S 002  | 75.00    |
| S 001  | 50.00    |
| S 005  | 40.00    |
| S 003  | NULL     |

---

Verification Queries

View All Tables
```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public';
```

View Table Structure (SQL)
```sql
SELECT column_name, data_type, character_maximum_length
FROM information_schema.columns
WHERE table_name = 'supplier';
```

Count Records
```sql
SELECT COUNT(*) AS SupplierCount FROM SUPPLIER;
SELECT COUNT(*) AS PartCount FROM PART;
SELECT COUNT(*) AS SupplierPartCount FROM SUPPLIER_PART;
```
