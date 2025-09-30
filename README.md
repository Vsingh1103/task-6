# task-6
# SQL Subqueries Practice
##  Objective  
- Learn to use **subqueries** in different SQL clauses: `SELECT`, `WHERE`, and `FROM`.  
- Strengthen query-building skills with **scalar**, **correlated**, and **nested logic**.  



## Tools  
- DB Browser for SQLite  
- MySQL Workbench  



## Database Schema  

### **Departments**
| Column         | Type         | Description                  |
|----------------|--------------|------------------------------|
| DepartmentID   | INT (PK)     | Unique ID for department     |
| DepartmentName | VARCHAR(100) | Name of department           |
| Location       | VARCHAR(100) | Department location          |

### **Employees**
| Column       | Type          | Description                   |
|--------------|---------------|-------------------------------|
| EmployeeID   | INT (PK)      | Unique ID for employee        |
| Name         | VARCHAR(100)  | Employee name                 |
| DepartmentID | INT (FK)      | References Departments table  |
| Salary       | DECIMAL(10,2) | Employee salary               |

---

## Sample Data  

**Departments**
| DepartmentID | DepartmentName | Location   |
|--------------|----------------|------------|
| 1            | HR             | New York   |
| 2            | Finance        | London     |
| 3            | IT             | New York   |
| 4            | Marketing      | Sydney     |

**Employees**
| EmployeeID | Name     | DepartmentID | Salary  |
|------------|----------|--------------|---------|
| 101        | Alice    | 1            | 60000   |
| 102        | Bob      | 2            | 75000   |
| 103        | Charlie  | 3            | 90000   |
| 104        | David    | 3            | 85000   |
| 105        | Eva      | 4            | 70000   |
| 106        | Frank    | 2            | 95000   |
| 107        | Grace    | 1            | 50000   |

---

## Example Queries with Subqueries  

-- Subquery in `SELECT` (Scalar Subquery)  
  
SELECT 
    e.EmployeeID,
    e.Name,
    e.Salary,
    (SELECT AVG(Salary) FROM Employees) AS AvgSalary
FROM Employees e;

-- 1. Create Departments table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(100),
    Location VARCHAR(100)
);

-- 2. Create Employees table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    DepartmentID INT,
    Salary DECIMAL(10,2),
    FOREIGN KEY (DepartmentID) REFERENCES Departments(DepartmentID)
);

-- 3. Insert Departments data
INSERT INTO Departments (DepartmentID, DepartmentName, Location) VALUES
(1, 'HR', 'New York'),
(2, 'Finance', 'London'),
(3, 'IT', 'New York'),
(4, 'Marketing', 'Sydney');


-- 4. Insert Employees data
INSERT INTO Employees (EmployeeID, Name, DepartmentID, Salary) VALUES
(101, 'Alice', 1, 60000),
(102, 'Bob', 2, 75000),
(103, 'Charlie', 3, 90000),
(104, 'David', 3, 85000),
(105, 'Eva', 4, 70000),
(106, 'Frank', 2, 95000),
(107, 'Grace', 1, 50000);


-- 5. Verify Data
SELECT * FROM Departments;
SELECT * FROM Employees;
