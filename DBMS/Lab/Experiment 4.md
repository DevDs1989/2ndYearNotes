# DBMS Lab Experiment 04
## To understand and apply the concept of Constraints
---
- **Course:** DBMS
- **Name:** Devesh Chandra Srivastava
- **SapID:** 590017127
- **Batch:** 66
- **Semester:** 3
- **Date:** 2025-10-06
---

## Objective
To understand the concept of data constraints that is enforced on data being stored in the table. Focus on Primary Key and the Foreign Key.

---

## ER → Relational Mapping

**Relations:**

1. **CLIENT_MASTER**(<u>ClientNo</u>, Name, City, State, Pincode, BalDue, Telephone)
2. **PRODUCT_MASTER**(<u>ProductNo</u>, Description, ProfitPercent, UnitMeasure, QtyOnHand, ReorderLvl, SellPrice, CostPrice)
3. **SALESMAN_MASTER**(<u>SalesmanNo</u>, Name, City, Pincode, State, SalAmt, TgtToGet, YtdSales, Remarks)

*Note: Primary keys are underlined. Foreign keys would be added when creating order tables.*

---

## 1. Table Creation

### Creating CLIENT_MASTER Table
```sql
CREATE TABLE CLIENT_MASTER (
    ClientNo VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    City VARCHAR(30),
    State VARCHAR(30),
    Pincode VARCHAR(10),
    BalDue DECIMAL(10, 2) DEFAULT 0
);
```

### Creating PRODUCT_MASTER Table
```sql
CREATE TABLE PRODUCT_MASTER (
    ProductNo VARCHAR(10) PRIMARY KEY,
    Description VARCHAR(100),
    ProfitPercent DECIMAL(5, 2),
    UnitMeasure VARCHAR(20),
    QtyOnHand INT,
    ReorderLvl INT,
    SellPrice DECIMAL(8, 2),
    CostPrice DECIMAL(8, 2)
);
```

### Creating SALESMAN_MASTER Table
```sql
CREATE TABLE SALESMAN_MASTER (
    SalesmanNo VARCHAR(10) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    City VARCHAR(30),
    Pincode VARCHAR(10),
    State VARCHAR(30),
    SalAmt DECIMAL(10, 2),
    TgtToGet DECIMAL(10, 2),
    YtdSales DECIMAL(10, 2),
    Remarks VARCHAR(100)
);
```

---

## 2. Inserting Sample Data

### Data for CLIENT_MASTER
```sql
INSERT INTO CLIENT_MASTER (ClientNo, Name, City, State, Pincode, BalDue) VALUES
('C00001', 'Ivan Bayross', 'Mumbai', 'Maharashtra', '400054', 15000.00),
('C00002', 'Mamta Muzumdar', 'Madras', 'Tamil Nadu', '780001', 0.00),
('C00003', 'Chhaya Bankar', 'Mumbai', 'Maharashtra', '400057', 5000.00),
('C00004', 'Ashwini Joshi', 'Bangalore', 'Karnataka', '560001', 0.00),
('C00005', 'Hansel Colaco', 'Mumbai', 'Maharashtra', '400060', 2000.00),
('C00006', 'Deepak Sharma', 'Mangalore', 'Karnataka', '560050', 0.00);
```

### Data for PRODUCT_MASTER
```sql
INSERT INTO PRODUCT_MASTER (ProductNo, Description, ProfitPercent, UnitMeasure, QtyOnHand, ReorderLvl, SellPrice, CostPrice) VALUES
('P00001', 'T-Shirts', 5.00, 'Piece', 200, 50, 350.00, 250.00),
('P0345', 'Shirts', 6.00, 'Piece', 150, 50, 500.00, 350.00),
('P06734', 'Cotton Jeans', 5.00, 'Piece', 100, 20, 600.00, 450.00),
('P07865', 'Jeans', 5.00, 'Piece', 100, 20, 750.00, 500.00),
('P07868', 'Trousers', 2.00, 'Piece', 150, 50, 850.00, 550.00),
('P07885', 'Pull Overs', 2.50, 'Piece', 80, 30, 700.00, 450.00),
('P07965', 'Denim Shirts', 4.00, 'Piece', 100, 40, 350.00, 250.00),
('P07975', 'Lycra Tops', 5.00, 'Piece', 70, 30, 300.00, 175.00),
('P08865', 'Skirts', 5.00, 'Piece', 75, 30, 450.00, 300.00);
```

### Data for SALESMAN_MASTER
```sql
INSERT INTO SALESMAN_MASTER (SalesmanNo, Name, City, Pincode, State, SalAmt, TgtToGet, YtdSales, Remarks) VALUES
('S00001', 'Aman', 'Mumbai', '400001', 'Maharashtra', 3000.00, 100000.00, 50000.00, 'Good'),
('S00002', 'Omkar', 'Mumbai', '400002', 'Maharashtra', 3000.00, 200000.00, 100000.00, 'Good'),
('S00003', 'Raj', 'Mumbai', '400003', 'Maharashtra', 3000.00, 200000.00, 100000.00, 'Good'),
('S00004', 'Ashish', 'Mumbai', '400004', 'Maharashtra', 3500.00, 200000.00, 150000.00, 'Good');
```

---

## 3. Exercise on Retrieving Records

### Q 1: Find out the names of all the clients


```sql
SELECT Name FROM CLIENT_MASTER;
```

#### Result
| Name |
|------|
| Ivan Bayross |
| Mamta Muzumdar |
| Chhaya Bankar |
| Ashwini Joshi |
| Hansel Colaco |
| Deepak Sharma |

---

### Q 2: Retrieve the entire contents of the Client_Master table


```sql
SELECT * FROM CLIENT_MASTER;
```

#### Result
| ClientNo | Name | City | State | Pincode | BalDue |
|----------|------|------|-------|---------|--------|
| C 00001 | Ivan Bayross | Mumbai | Maharashtra | 400054 | 15000.00 |
| C 00002 | Mamta Muzumdar | Madras | Tamil Nadu | 780001 | 0.00 |
| ... | ... | ... | ... | ... | ... |

---

### Q 3: Retrieve the list of names, city and state of all the clients


```sql
SELECT Name, City, State FROM CLIENT_MASTER;
```

#### Result
| Name | City | State |
|------|------|-------|
| Ivan Bayross | Mumbai | Maharashtra |
| Mamta Muzumdar | Madras | Tamil Nadu |
| Chhaya Bankar | Mumbai | Maharashtra |
| ... | ... | ... |

---

### Q 4: List the various products available from the Product_Master table



```sql
SELECT Description FROM PRODUCT_MASTER;
```

#### Result
| Description |
|-------------|
| T-Shirts |
| Shirts |
| Cotton Jeans |
| Jeans |
| Trousers |
| ... |

---

### Q 5: List all the clients who are located in Mumbai


```sql
SELECT * FROM CLIENT_MASTER 
WHERE City = 'Mumbai';
```

#### Result
| ClientNo | Name | City | State | Pincode | BalDue |
|----------|------|------|-------|---------|--------|
| C 00001 | Ivan Bayross | Mumbai | Maharashtra | 400054 | 15000.00 |
| C 00003 | Chhaya Bankar | Mumbai | Maharashtra | 400057 | 5000.00 |
| C 00005 | Hansel Colaco | Mumbai | Maharashtra | 400060 | 2000.00 |

---

### Q 6: Find the names of salesman who have a salary equal to Rs. 3000

```sql
SELECT Name FROM SALESMAN_MASTER 
WHERE SalAmt = 3000.00;
```

#### Result
| Name |
|------|
| Aman |
| Omkar |
| Raj |

---

## 4. Exercise on Updating Records

### Q 1: Change the city of ClientNo 'C 00005' to 'Bangalore'


```sql
UPDATE CLIENT_MASTER 
SET City = 'Bangalore' 
WHERE ClientNo = 'C00005';
```

---

### Q 2: Change the BalDue of ClientNo 'C 00001' to Rs. 1000

```sql
UPDATE CLIENT_MASTER 
SET BalDue = 1000.00 
WHERE ClientNo = 'C00001';
```

---

### Q 3: Change the cost price of 'Trousers' to Rs. 950.00

```sql
UPDATE PRODUCT_MASTER 
SET CostPrice = 950.00 
WHERE Description = 'Trousers';
```

---

### Q 4: Change the city of the salesman to Pune


```sql
UPDATE SALESMAN_MASTER 
SET City = 'Pune';
```

---

## 5. Exercise on Deleting Records

### Q 1: Delete all salesman whose salaries are equal to Rs. 3500
```sql
DELETE FROM SALESMAN_MASTER 
WHERE SalAmt = 3500.00;
```

---

### Q 2: Delete all products where quantity on hand is equal to 100


```sql
DELETE FROM PRODUCT_MASTER 
WHERE QtyOnHand = 100;
```

---

### Q 3: Delete from Client_Master where state is 'Tamil Nadu'


```sql
DELETE FROM CLIENT_MASTER 
WHERE State = 'Tamil Nadu';
```

---

## 6. Exercise on Altering Table Structure

### Q 1: Add a column called 'Telephone' to Client_Master table


```sql
ALTER TABLE CLIENT_MASTER 
ADD Telephone BIGINT;
```

---

### Q 2: Change the size of SellPrice column to 10,2

```sql
ALTER TABLE PRODUCT_MASTER 
ALTER COLUMN SellPrice TYPE DECIMAL(10, 2);
```

---

## 7. Exercise on Deleting Table Structure

### Q 1: Destroy the table Client_Master along with its data

```sql
DROP TABLE CLIENT_MASTER;
```

---

## Verification Queries

### View All Tables
```sql
SELECT table_name 
FROM information_schema.tables 
WHERE table_schema = 'public';
```

### View Table Structure
```sql
-- Using psql meta-command
\d CLIENT_MASTER
\d PRODUCT_MASTER
\d SALESMAN_MASTER

-- Using SQL query
SELECT column_name, data_type, character_maximum_length
FROM information_schema.columns
WHERE table_name = 'client_master';
```

### Count Records
```sql
SELECT COUNT(*) AS ClientCount FROM CLIENT_MASTER;
SELECT COUNT(*) AS ProductCount FROM PRODUCT_MASTER;
SELECT COUNT(*) AS SalesmanCount FROM SALESMAN_MASTER;
```

---
